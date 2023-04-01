# S0ix states
_S0ix-states_ represent the residency in the Intel® SoC idle standby power states. The S0ix states shut off parts of the SoC when they are not in use, while still maintaining optimal performance. These states are triggered when specific conditions within the SoC have been achieved, for example, when certain components are in low power states.

From an ACPI-compatible-OS point of view (see [[ACPI Power States]]), S0ix is an idle condition while still in “S0 active” state.

However, S0ix is not totally transparent to the OS. In order to enter the S0ix state, there are specific platform-dependent conditions the OS must meet. For this purpose, the [ACPI 6.2 Specification](http://uefi.org/sites/default/files/resources/ACPI_6_2.pdf) introduced a Low Power S0 Idle Capable Flag in the Fixed ACPI Description Table (FADT). For x86 systems, this flag informs the OS whether an Intel® SoC has S0ix support or not.

From the hardware perspective, the SLP_S0# signal indicates that the system has entered the deepest S0ix state.