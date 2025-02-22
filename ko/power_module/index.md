# Power Modules & Power Distribution Boards

_Power Modules_ provide a regulated power supply for the flight controller (FC), along with information about battery voltage and current. 전압/전류 정보는 소비 전력을 확인하고 남은 배터리 용량을 추정합니다. 비행 콘트롤러의 전력 부족시 안전 경고 및 기타 조치를 제공합니다: [안전 &gt; 배터리 부족 안전장치](../config/safety.md#low-battery-failsafe).

_Power Distribution Boards (PDB)_ are circuit boards that may be used to simplify splitting the output of the battery to various parts of the drone, and in particular motors. PDBs will sometimes include a power module for the FC, ESCs for motors, and a battery elimination circuit (BEC) for powering servos.

PX4 배터리/전원 모듈 설정 방법(ADC 인터페이스를 통한)은 [전원모듈 설정](../config/battery.md)을 참고하십시오.

::: tip
For easiest assembly use a power module or PDB recommended by your FC manufacturer, and sized for your power requirements.

The Pixhawk connector standard requires that the VCC line must provide at least 2.5A continuous current and default to 5.3V. In in practice flight controllers may have different recommendations or preferences, so if you don't (or can't) use a recommended module, check that the module matches your FC's requirements.
:::

This section provides information about a number of power modules and power distribution boards (see FC manufacturer docs for more options):

* 아날로그 전압 및 전류 전력 모듈 :
  * [CUAV HV PM](../power_module/cuav_hv_pm.md)
  * [Holybro PM02](../power_module/holybro_pm02.md)
  * [Holybro PM07](../power_module/holybro_pm07_pixhawk4_power_module.md)
  * [Holybro PM06 V2](../power_module/holybro_pm06_pixhawk4mini_power_module.md)
  * [Sky-Drones SmartAP PDB](../power_module/sky-drones_smartap-pdb.md)
* Digital (I2C) voltage and current power modules (for Pixhawk FMUv6X and FMUv5X derived controllers):
  * [Holybro PM02D](../power_module/holybro_pm02d.md)
  * [Holybro PM03D](../power_module/holybro_pm03d.md)
* [DroneCAN](../dronecan/index.md) power modules
  * [CUAV CAN PMU](../dronecan/cuav_can_pmu.md)
  * [Pomegranate Systems Power Module](../dronecan/pomegranate_systems_pm.md)
