# DJI FlameWheel 450 + CUAV V5 nano 조립

키트 조립법과 *QGroundControl*의 PX4 설정법을 설명합니다.

주요 정보

- **프레임:** DJI F450
- **비행 컨트롤러:** [CUAV V5 nano](../flight_controller/cuav_v5_nano.md)
- **조립 시간 (예상):** 90분 (프레임 조립에 45분, 오토파일럿 설치와 설정에 45분)

![성절 완료하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/f450_cuav5_nano_complete.jpg)

## 부품 명세서

조립에 필요한 부품들입니다.
- Flight controller: [CUAV V5 nano](https://store.cuav.net/shop/v5-nano/):
  - GPS: [CUAV NEO V2 GPS](https://store.cuav.net/index.php?id_product=97&id_product_attribute=0&rewrite=cuav-new-ublox-neo-m8n-gps-module-with-shell-stand-holder-for-flight-controller-gps-compass-for-pixhack-v5-plus-rc-parts-px4&controller=product&id_lang=1)
  - 전원 모듈
- 프레임: [DJI F450](https://www.amazon.com/Flame-Wheel-Basic-Quadcopter-Drone/dp/B00HNMVQHY)
- Propellers: [DJI Phantom Built-in Nut Upgrade Propellers 9.4x5](https://www.masterairscrew.com/products/dji-phantom-built-in-nut-upgrade-propellers-in-black-mr-9-4x5-prop-set-x4-phantom)
- 배터리: [Turnigy High Capacity 5200mAh 3S 12C Lipo Pack w/XT60](https://hobbyking.com/en_us/turnigy-high-capacity-5200mah-3s-12c-multi-rotor-lipo-pack-w-xt60.html?___store=en_us)
- Telemetry: [Holybro Transceiver Telemetry Radio V3](../telemetry/holybro_sik_radio.md)
- RC 수신기: [FrSky D4R-II 2.4G 4CH ACCST Telemetry Receiver](https://www.banggood.com/FrSky-D4R-II-2_4G-4CH-ACCST-Telemetry-Receiver-for-RC-Drone-FPV-Racing-p-929069.html?cur_warehouse=GWTR)
- Motors: [DJI E305 2312E Motor (960kv,CW)](https://www.amazon.com/DJI-E305-2312E-Motor-960kv/dp/B072MBMCZN)
- ESC: Hobbywing XRotor 20A APAC Brushless ESC 3-4S For RC Multicopters


FrSky Taranis 조종기를 사용할 수 있습니다. 부수적으로 케이블 타이와, 양면 테이프, 납땜도 필요합니다.

아래의 이미지는 프레임과 전자 부품들을 나타냅니다.

![이 구성에 사용된 모든 부품들](../../assets/airframes/multicopter/dji_f450_cuav_5nano/all_components.jpg)


## 하드웨어

### 프레임

이 절에서는 에어 프레임의 모든 하드웨어를 나열합니다.

| 품목                                 | 수량 |
| ---------------------------------- | -- |
| DJI F450 밑판                        | 1  |
| DJI F450 윗판                        | 1  |
| DJI F450 랜딩기어 역할을 하는 다리            | 4  |
| M3*8 나사                            | 18 |
| M2 5*6 나사                          | 24 |
| 벨크로 배터리 스트랩                        | 1  |
| DJI Phantom 나사 내장 업그레이드 프로펠러 9.4x5 | 1  |

![F450 프레임 부품들](../../assets/airframes/multicopter/dji_f450_cuav_5nano/f450_frame_components.png)


### CUAV v5 nano 패키지

이 절에서는 CUAV v5 나노 구성 모음의 부품을 나열합니다.

| 품목                  | 수량 (기본 패키지) | 수량 (+GPS 패키지) |
| ------------------- | ----------- | ------------- |
| V5 nano 비행 제어기      | 1           | 1             |
| 듀퐁 케이블              | 2           | 2             |
| I2C/CAN 케이블         | 2           | 2             |
| ADC 6.6 케이블         | 2           | 2             |
| SBUS 시그널 케이블        | 1           | 1             |
| IRSSI 케이블           | 1           | 1             |
| DSM 시그널 케이블         | 1           | 1             |
| ADC 3.3 케이블         | 1           | 1             |
| Debug 케이블           | 1           | 1             |
| 안전 스위치 케이블          | 1           | 1             |
| 전압 & 전류 케이블         | 1           | 1             |
| PW-Link 모듈 케이블      | 1           | 1             |
| 전원 모듈               | 1           | 1             |
| SanDisk 16GB 메모리 카드 | 1           | 1             |
| I2C 확장 보드           | 1           | 1             |
| TTL Plate           | 1           | 1             |
| NEO GPS             | -           | 1             |
| GPS 브라켓             | -           | 1             |


### 전자부품

| 품목                                             | 수량 |
| ---------------------------------------------- | -- |
| CUAV V5 nano                                   | 1  |
| CUAV NEO V2 GPS                                | 1  |
| Holibro 텔레메트리                                  | 1  |
| FrSky D4R-II 2.4G 4CH ACCST Telemetry Receiver | 1  |
| DJI E305 2312E Motor (800kv,CW)                | 4  |
| Hobbywing XRotor 20A APAC Brushless ESC        | 4  |
| 전원모듈(CUAV V5 nano 패키지에 포함)                     | 1  |
| Turnigy 고용량 5200mAh 3S 12C Lipo Pack w/XT60    | 1  |


### 필요한 공구

조립시에 필요한 공구들입니다.

- 2.0mm 육각 스크류드라이버
- 3mm Phillips 스크류드라이버
- Wire 커터
- 정밀 트위저
- 납땜기


![필요 공구들](../../assets/airframes/multicopter/dji_f450_cuav_5nano/required_tools.jpg)

## 조립

예상 조립 시간은 약 90분입니다 (프레임 조립에 약 45분, 자율비행프로그램 설치와 설정에 약 45분).

1. 제공된 나사를 이용하여 하판에 팔 4개를 결합합니다.

   ![밑판의 팔들](../../assets/airframes/multicopter/dji_f450_cuav_5nano/1_attach_arms_bottom_plate.jpg)

1. ESC (변속기) 의 양극 (빨강)과 음극 (검정)을 보드에 납땜합니다.

   ![ESC 납땜하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/2_solder_esc.jpg)

1. 전원 모듈의 양극 (빨강)과 음극 (검정)을 납땜합니다.

   ![전원 모듈 납땜하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/3_solder_power_module.jpg)

1. 위치에 따라 모터를 ESC에 연결합니다.

   ![모터 연결하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/4_plug_in_motors.jpg)

1. 각각의 모터를 해당하는 팔에 고정합니다.

   ![팔(흰색) 에 모터 장착하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/5a_attach_motors_to_arms.jpg) ![팔(빨간색) 에 모터 장착하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/5b_attach_motors_to_arms.jpg)

1. (다리의 윗부분과 나사로 결합하여) 상판을 장착합니다.

   ![상판 장착](../../assets/airframes/multicopter/dji_f450_cuav_5nano/6_add_top_board.jpg)

1. 진동 방지 폼테이프를 *CUAV V5 nano* 비행 컨트롤러에 부착합니다.

   ![진동방지 폼테이프](../../assets/airframes/multicopter/dji_f450_cuav_5nano/7a_attach_cuav5nano.jpg) ![진동방지 폼테이프](../../assets/airframes/multicopter/dji_f450_cuav_5nano/7b_attach_cuav5nano.jpg)

1. FrSky 수신기를 양면 테이프를 이용하여 하판에 부착합니다.

   ![양면테이프로 FrSky 수신기 부착하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/8_attach_frsky.jpg)

1. 텔레메트리 모듈을 기체의 아랫판에 양면테이프를 이용하여 부착합니다.

   ![무선 텔레메트리 장착하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/9a_telemtry_radio.jpg) ![무선 텔레메트리 장착하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/9b_telemtry_radio.jpg)

1. 알루미늄 GPS 지지대를 밑판에 추가한후 GPS를 부착합니다.

   ![알루미늄 지지대](../../assets/airframes/multicopter/dji_f450_cuav_5nano/10_aluminium_standoffs.jpg)

1. 비행컨트롤러의 각 포트에 맞게 텔레메트리는 (`TELEM1`) 에, GPS 모듈은 (`GPS/SAFETY`) 에, RC 수신기는 (`RC`) 에, 모든 4 ESC’s (`M1-M4`) 에, 그리고 전원 모듈은(`Power1`) 꽂습니다. ![비행 컨트롤러에 주변장치 장착하기](../../assets/airframes/multicopter/dji_f450_cuav_5nano/12_fc_attach_periperhals.jpg)

   ::: info The motor order is defined in the [Airframe Reference > Quadrotor x](../airframes/airframe_reference.md#quadrotor-x)
:::

끝났습니다! 마지막 조립순서가 다음에 이어집니다:

![성절 완료](../../assets/airframes/multicopter/dji_f450_cuav_5nano/f450_cuav5_nano_complete.jpg)


## PX4 Configuration

*QGroundControl*에서 PX4 자율비행 프로그램을 설치하고 프레임에 대한 설정과 보정 작업을 진행합니다. [Download and install](http://qgroundcontrol.com/downloads/) *QGroundControl* for your platform.

:::tip PX4 설치 및 성정 매뉴얼은 [기본 설정](../config/README.md)편을 참고하십시오.
:::

First update the firmware, airframe, geometry and outputs:

- [펌웨어](../config/firmware.md)
- [Airframe](../config/airframe.md)

  ::: info You will need to select the *Generic Quadcopter* airframe (**Quadrotor x > Generic Quadcopter**).

  ![QGroundControl - Select Generic Quadcopter](../../assets/airframes/multicopter/dji_f450_cuav_5nano/qgc_airframe_generic_quadx.png)
:::

- [Actuators](../config/actuators.md)
  - Update the vehicle geometry to match the frame.
  - Assign actuator functions to outputs to match your wiring.
  - Test the configuration using the sliders.


그리고, 설치후에 필수적인 설정 작업과 보정 작업을 진행하여야 합니다.

- [센서 방향](../config/flight_controller_orientation.md)
- [나침반](../config/compass.md)
- [가속도계](../config/accelerometer.md)
- [수평 보정](../config/level_horizon_calibration.md)
- [무선 조종기 설정](../config/radio.md)
- [비행 모드](../config/flight_mode.md)

  ::: info For this build we set up modes *Stabilized*, *Altitude* and *Position* on a three-way switch on the receiver (mapped to a single channel - 5). 이 방법이 초심자에게 추천하는 최소 설정입니다.
:::

이후 다음 작업 역시 수행되어야 합니다:

- [ESC 보정](../advanced_config/esc_calibration.md)
- [배터리](../config/battery.md)
- [안전 설정](../config/safety.md)


## 튜닝

Airframe selection sets *default* autopilot parameters for the frame. These may be good enough to fly with, but you should tune each frame build.

For instructions on how, start from [Autotune](../config/autotune_mc.md).


## 비디오

@[유투브](https://youtu.be/b0bKNdDqVHw)


## 감사의 글

이 빌드 로그는 Dronecode Test Flight Team에서 제공했습니다.
