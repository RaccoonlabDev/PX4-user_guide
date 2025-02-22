# Gazebo 仿真

:::warning
Gazebo 先前被称为“Gazebo Ignition”( _Gazebo Classic_ 先前被称为Gazebo)。 查看 [官方博客文章](https://www.openrobotics.org/blog/2022/4/6/a-new-era-for-gazebo) 获取更多信息。
:::

[Gazebo](https://gazebosim.org/home) 是一个开源机器人模拟器。 它取代了旧的 [Gazebo Classic](../sim_gazebo_classic/README.md) 模拟器，是Ubuntu 22.04 及以后唯一支持的 Gazebo 版本。

**支持的载具：** Quadrotor、Plane、VTOL

@[youtube](https://youtu.be/eRzdGD2vgkU)

::: info
See [Simulation](../simulation/index.md) for general information about simulators, the simulation environment, and simulation configuration (e.g. supported vehicles).
:::

## Installation (Ubuntu Linux)

Gazebo is installed by default on Ubuntu 22.04 as part of the normal [development environment setup](../dev_setup/dev_env_linux_ubuntu.md#simulation-and-nuttx-pixhawk-targets).

If you want to use Gazebo on Ubuntu 20.04 you can install it manually, after first following the normal setup process (installing `gz-garden` will uninstall Gazebo-Classic!):

```sh
sudo wget https://packages.osrfoundation.org/gazebo.gpg -O /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null
sudo apt-get update
sudo apt-get install gz-garden
```

## Running the Simulation

Gazebo SITL simulation can be conveniently run using a `make` command as shown below:

```sh
cd /path/to/PX4-Autopilot
make px4_sitl gz_x500
```

This runs both the PX4 SITL instance and the Gazebo client.

The supported vehicles and `make` commands are listed below. Note that all gazebo make targets have the prefix `gz_`.

| Vehicle                                                                                                  | Command                           | `PX4_SYS_AUTOSTART` |
| -------------------------------------------------------------------------------------------------------- | --------------------------------- | ------------------- |
| [Quadrotor(x500)](../sim_gazebo_gz/vehicles.md#x500-quadrotor)                                           | `make px4_sitl gz_x500`           | 4001                |
| [Quadrotor(x500) with Depth Camera](../sim_gazebo_gz/vehicles.md#x500-quadrotor-with-depth-camera)       | `make px4_sitl gz_x500_depth`     | 4002                |
| [Quadrotor(x500) with Vision Odometry](../sim_gazebo_gz/vehicles.md#x500-quadrotor-with-visual-odometry) | `make px4_sitl gz_x500_vision`    | 4005                |
| [VTOL](../sim_gazebo_gz/vehicles.md#standard-vtol)                                                       | `make px4_sitl gz_standard_vtol`  | 4004                |
| [Plane](../sim_gazebo_gz/vehicles.md#standard-plane)                                                     | `make px4_sitl gz_rc_cessna`      | 4003                |
| [Advanced Plane](../sim_gazebo_gz/vehicles.md#advanced-plane)                                            | `make px4_sitl gz_advanced_plane` | 4008                |

All [vehicle models](../sim_gazebo_gz/vehicles.md) (and [worlds](#specify-world)) are included as a submodule from the [Gazebo Models Repository](../sim_gazebo_gz/gazebo_models.md) repository.

:::warning
The Advanced Lift Drag Plugin that is required to run the Advanced Plane is not yet part of the Gazebo distribution, so the Advanced Plane will not yet fly: [PX4-Autopilot#22337](https://github.com/PX4/PX4-Autopilot/issues/22337).

As a workaround to enable Advanced Plane, you can compile the gz-sim library from [Gazebo source code](https://github.com/gazebosim/gz-sim), go into the `build/lib` directory, copy out the advanced lift drag plugin `.so` file (depending on the exact Gazebo Version this is called something along the lines of `libgz-sim7-advanced-lift-drag-system.so`), and paste this into the `~/.gz/sim/plugins` folder.
:::

The commands above launch a single vehicle with the full UI. _QGroundControl_ should be able to automatically connect to the simulated vehicle.

### Standalone Mode

Another way that Gazebo SITL can be connected is in _standalone mode_. In this mode PX4 SITL and Gazebo are started separately in their own terminals. By default these terminals are on the same host, but you can also connect SITL and Gazebo instances running on any two devices on the network (or even different networks if you use a VPN to connect them).

You start PX4 in standalone mode by prefixing the `make` command with `PX4_GZ_STANDALONE=1`:

```sh
cd /path/to/PX4-Autopilot
PX4_GZ_STANDALONE=1 make px4_sitl gz_x500
```

PX4 SITL will then wait until it detects an instance of _gz-server_, and then connect to it.

::: info
If you have not yet started _gz-server_ when you run the `make` command, you will see the following warning until gazebo has been started and an instance of _gz-server_ is detected by PX4:

```sh
WARN [gz bridge] Service call timed out as Gazebo has not been detected
```

:::

The simplest way to start the simulation is to use the Python script [simulation-gazebo](https://github.com/PX4/PX4-gazebo-models/blob/main/simulation-gazebo), which can be found in the [Gazebo Models Repository](../sim_gazebo_gz/gazebo_models.md) repository. This can be used to launch a _gz-server_ instance with any supported world and vehicle.

The script can be used without installing any additional dependencies, and will fetch the supported PX4 models and worlds on first use (by default) and save them to `~/.simulation-gazebo`. If called again the script will use this directory to get models and worlds. Therefore if you want to use your own model and run it in standalone mode, you will have to place its source code in `~/.simulation-gazebo`.

You can fetch the script locally using any method you like, such as `wget`:

```sh
wget https://raw.githubusercontent.com/PX4/PX4-gazebo-models/main/simulation-gazebo
```

The script can be started with:

```sh
cd /path/to/script/
python3 simulation-gazebo
```

For more information and arguments, see [Gazebo Models](../sim_gazebo_gz/gazebo_models.md).

::: info
If `make px4_sitl gz_x500` gives the error `ninja: error: unknown target 'gz_x500'` then run `make distclean` to start from a clean slate, and try running `make px4_sitl gz_x500` again.
:::

### Headless Mode

You might want to run Gazebo in "headless mode" (without the Gazebo GUI) as it uses fewer resources, and does not rely on your system having a graphics card that properly supports OpenGL rendering. This makes it faster to load and run, and for many simple use cases may be all you need.

The simulation can be run in headless mode by prefixing the command with the `HEADLESS=1` environment variable:

```sh
HEADLESS=1 make px4_sitl gz_x500
```

### Specify World

The simulation can be run inside a particular world by concatenating the desired world to the name of the desired vehicle. For example, to run the windy world with the `x500` vehicle you can specify:

```sh
make px4_sitl gz_x500_windy
```

You can also specify the world using the `PX4_GZ_WORLD` environment variable:

```sh
PX4_GZ_WORLD=windy make px4_sitl gz_x500
```

The supported worlds are listed below.

| World      | Command                    | Description                        |
| ---------- | -------------------------- | ---------------------------------- |
| `default`  | `make px4_sitl *`          | Empty world (a grey plane)         |
| `windy`    | `make px4_sitl *_windy`    | Empty world with wind enabled      |
| `baylands` | `make px4_sitl *_baylands` | Baylands world surrounded by water |

:::warning
Note that if no world is specified, PX4 will use the `default` world. However you must not _explicitly_ specify `_default` on the model as this will prevent PX4 from launching. In other words, use `make px4_sitl gz_x500` instead of `make px4_sitl gz_x500_default` for the default.
:::

::: info
Baylands throws the following error, which can be ignored:

```
[Err] [SDFFeatures.cc:843] The geometry element of collision [collision] couldn't be created
```

This occurs because Baylands has a lot of meshes. However it does not break Gazebo and the error has been downgraded to a warning in Gazebo Harmonic: [gz-physics/pull/531](https://github.com/gazebosim/gz-physics/pull/531). You can also replace the error with a warning by [installing gz-garden from source](https://gazebosim.org/docs/garden/install_ubuntu_src).
:::

## Usage/Configuration Options

The startup pipeline allows for highly flexible configuration. In particular, it is possible to:

- Start a new simulation with an arbitrary world or attach to an already running simulation.
- Add a new vehicle to the simulation or link a new PX4 instance to an existing one.

These scenarios are managed by setting the appropriate environment variables.

### Syntax

The startup syntax takes the form:

```sh
ARGS ./build/px4_sitl_default/bin/px4
```

where `ARGS` is a list of environment variables including:

- `PX4_SYS_AUTOSTART` (**Mandatory**): Sets the [airframe autostart id](../dev_airframes/adding_a_new_frame.md) of the PX4 airframe to start.

- `PX4_GZ_MODEL_NAME`: Sets the name of an _existing_ model in the gazebo simulation. If provided, the startup script tries to bind a new PX4 instance to the Gazebo resource matching exactly that name.

  - The setting is mutually exclusive with `PX4_SIM_MODEL`.

- `PX4_SIM_MODEL`: Sets the name of a new Gazebo model to be spawned in the simulator. If provided, the startup script looks for a model in the Gazebo resource path that matches the given variable, spawns it and binds a new PX4 instance to it.

  - The setting is mutually exclusive with `PX4_GZ_MODEL_NAME`.

  ::: info The environmental variable `PX4_GZ_MODEL` has been deprecated and its functionality merged into `PX4_SIM_MODEL`.
:::

- `PX4_GZ_MODEL_POSE`: Sets the spawning position and orientation of the model when `PX4_SIM_MODEL` is adopted. If provided, the startup script spawns the model at a pose following the syntax `"x,y,z,roll,pitch,yaw"`, where the positions are given in metres and the angles are in radians.

  - If omitted, the zero pose `[0,0,0,0,0,0]` is used.
  - If less then 6 values are provided, the missing ones are fixed to zero.
  - This can only be used with `PX4_SIM_MODEL` (not `PX4_GZ_MODEL_NAME`).

- `PX4_GZ_WORLD`: Sets the Gazebo world file for a new simulation. If it is not given, then [default](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/simulation/gz/worlds/default.sdf) is used.

  - This variable is ignored if an existing simulation is already running.
  - This value should be [specified for the selected airframe](#adding-new-worlds-and-models) but may be overridden using this argument.

- `PX4_SIMULATOR=GZ`: Sets the simulator, which for Gazebo must be `gz`.

  - This value should be [set for the selected airframe](#adding-new-worlds-and-models), in which case it does not need to be set as an argument.

- `PX4_GZ_STANDALONE`: Lets PX4 know that it should not launch an instance of Gazebo. Gazebo will need to be launched separately, as described in [Standalone Mode](#standalone-mode).

- `PX4_GZ_SIM_RENDER_ENGINE`: Sets the render engine to be used by gazebo.

  The default rendering engine (OGRE 2) is not well supported on some platforms/environments. Specify `PX4_GZ_SIM_RENDER_ENGINE=ogre` to set the rendering engine to OGRE 1 if you have rendering issues when running PX4 on a virtual machine.

The PX4 Gazebo worlds and and models databases [can be found on Github here](https://github.com/PX4/PX4-gazebo-models).

::: info
`gz_env.sh.in` is compiled and made available in `$PX4_DIR/build/px4_sitl_default/rootfs/gz_env.sh`
:::

### Examples

Here are some examples of the different scenarios covered above.

1. **Start simulator + default world + spawn vehicle at default pose**

   ```sh
   PX4_SYS_AUTOSTART=4001 PX4_SIM_MODEL=gz_x500 ./build/px4_sitl_default/bin/px4
   ```

2. **Start simulator + default world + spawn vehicle at custom pose (y=2m)**

   ```sh
   PX4_SYS_AUTOSTART=4001 PX4_GZ_MODEL_POSE="0,2" PX4_SIM_MODEL=gz_x500 ./build/px4_sitl_default/bin/px4
   ```

3. **Start simulator + default world + link to existing vehicle**

   ```sh
   PX4_SYS_AUTOSTART=4001 PX4_GZ_MODEL_NAME=x500 ./build/px4_sitl_default/bin/px4
   ```

4. **Start simulator in standalone mode + connect to Gazebo instance running default world**

   ```sh
   PX4_GZ_STANDALONE=1 PX4_SYS_AUTOSTART=4001 PX4_SIM_MODEL=gz_x500 ./build/px4_sitl_default/bin/px4
   ```

   In a separate terminal run:

   ```sh
   python /path/to/simulation-gazebo
   ```

## Adding New Worlds and Models

SDF files, mesh files, textures and anything else to do with the functionality and appearance in Gazebo for worlds and models can be placed in the appropriate `/worlds` and `/models` directories in [PX4-gazebo-models](https://github.com/PX4/PX4-gazebo-models).

Within PX4 follow the below steps to add models and worlds.

### Adding a Model

To add a new model:

1. Define an [airframe configuration file](../dev_airframes/adding_a_new_frame.md).
1. Define the default parameters for Gazebo in the airframe configuration file (this example is from [x500 quadcopter](https://github.com/PX4/PX4-Autopilot/blob/main/ROMFS/px4fmu_common/init.d-posix/airframes/4001_gz_x500)):

   ```ini
   PX4_SIMULATOR=${PX4_SIMULATOR:=gz}
   PX4_GZ_WORLD=${PX4_GZ_WORLD:=default}
   PX4_SIM_MODEL=${PX4_SIM_MODEL:=<your model name>}
   ```

   - `PX4_SIMULATOR=${PX4_SIMULATOR:=gz}` sets the default simulator (Gz) for that specific airframe.
   - `PX4_GZ_WORLD=${PX4_GZ_WORLD:=default}` sets the [default world](https://github.com/PX4/PX4-Autopilot/blob/main/Tools/simulation/gz/worlds/default.sdf) for that specific airframe.

   - Setting the default value of `PX4_SIM_MODEL` lets you start the simulation with just:

     ```sh
     PX4_SYS_AUTOSTART=<your new airframe id> ./build/px4_sitl_default/bin/px4
     ```

1. Add CMake Target for the [airframe](https://github.com/PX4/PX4-Autopilot/blob/main/ROMFS/px4fmu_common/init.d-posix/airframes/CMakeLists.txt).

   - If you plan to use "regular" mode, add your model SDF to `Tools/simulation/gz/models/`.
   - If you plan to use _standalone_ mode, add your model SDF to `~/.simulation-gazebo/models/`

   You can of course also use both.

### Adding a World

To add a new world:

1. Add your world to the list of worlds found in the [`CMakeLists.txt` here](https://github.com/PX4/PX4-Autopilot/blob/main/src/modules/simulation/gz_bridge/CMakeLists.txt). This is required in order to allow `CMake` to generate correct targets.

   - If you plan to use "normal" mode, add your world sdf to `Tools/simulation/gz/worlds/`.
   - If you plan to use _standalone_ mode, add your world SDF to `~/.simulation-gazebo/worlds/`

::: info
As long as the world file and the model file are in the Gazebo search path (`GZ_SIM_RESOURCE_PATH`) it is not necessary to add them to the PX4 world and model directories. However, `make px4_sitl gz_<model>_<world>` won't work with them.
:::

## PX4-Gazebo Time Synchronization

Unlike the Gazebo Classic and jMAVSim simulators, PX4 and Gazebo do not implement a lockstep mechanism.

During Gazebo simulations PX4 subscribes to the Gazebo `\clock` topic and uses it as clock source. This guarantees that PX4 will always wait for Gazebo before moving forward in time, even if Gazebo is running with real time factors different from 1.

Note, however, that as the lockstep is missing, Gazebo will never wait for PX4 to finish its computations. In the worst case scenario, PX4 can completely go offline and Gazebo will keep running, with obvious crashes of the simulated drone.

## Multi-Vehicle Simulation

Multi-Vehicle simulation is supported on Linux hosts.

For more information see: [Multi-Vehicle Simulation with Gazebo](../sim_gazebo_gz/multi_vehicle_simulation.md)

## Further Information

- [px4-simulation-ignition](https://github.com/Auterion/px4-simulation-ignition)
