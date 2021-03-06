#####################################################
### Project configuration                          ##
### Values may be set using environmental variables ##
#####################################################

## COM_PORT: Serial port, required to flash firmware
COM_PORT ?= /dev/ttyS4

## COM_SPEED: Serial port baud rate
COM_SPEED ?= 115200

## COM_SPEED_ESPTOOL: Serial port baud rate used for flashing (defaults to COM_SPEED)
COM_SPEED_ESPTOOL ?= 115200

## DISABLE_SPIFFS: Set to 1 to disable SPIFFS file system
DISABLE_SPIFFS = 1
SPIFF_FILES = spiffs

## RBOOT_ENABLED: Set to 1 to use rboot boot loader (non-rboot will be deprecated)
RBOOT_ENABLED = 1

## RBOOT_BIG_FLASH: Set to 1 to allow ROM to be located in any 1MB block (not just first 1MB block)
RBOOT_BIG_FLASH = 1

## RBOOT_TWO_ROMS: Set to 1 to allow two ROMs to be located within first 1MB block
RBOOT_TWO_ROMS = 0

## RBOOT_RTC_ENABLED: Set to 1 to use RTC memory to communcate with rBoot
RBOOT_RTC_ENABLED = 0

## RBOOT_GPIO_ENABLED: Set to 1 to use a GPIO pin to select this ROM (do not set RBOOT_GPIO_SKIP_ENABLED)
## RBOOT_GPIO_SKIP_ENABLED: Set to 1 to use a GPIO pin to select next ROM (do not set RBOOT_GPIO_ENABLED)
## RBOOT_GPIO_NUMBER: Define GPIO pin to use for rBoot GPIO control
RBOOT_GPIO_ENABLED = 0

RBOOT_SILENT = 0

## MODULES: Source directories separated by space
MODULES = src

## EXTRA_INCDIR: Include directories separated by space
EXTRA_INCDIR = include

## VERBOSE: Set to 1 for more verbose build information
VERBOSE = 0

## ESP_HOME: Path where ESP tools and SDK are located.
ESP_HOME ?= ~/Sming/esp-toolkit/sdk

## SMING_HOME Path where Sming framework is located.
SMING_HOME ?= ~/Sming/Sming

## SPI_SIZE: ESP8266 flash memory size [512K | 1M | 2M | 4M]
SPI_SIZE ?= 4M

## SPI_SPEED: ESP8266 clock speed [40 | 80]
SPI_SPEED ?= 40

## SPI_MODE: ESP8266 transfer mode [qio | qout | dio | dout]
SPI_MODE ?= qio

## ENABLE_SSL: Set to 1 to use SSL features
ENABLE_SSL = 1

## ENABLE_ESPCONN: ESPCONN is used by some network features such as smartconfig when custom LWIP is used
ENABLE_ESPCONN = 1

## TERMINAL: Command to launch serial terminal interface with ESP8266
ifneq ($(filter CYGWIN%,$(shell uname -s)),)
TERMINAL     ?= mintty -t "ESP8266 Terminal" --bg 0,0,128 python -m serial.tools.miniterm $(COM_PORT) $(COM_SPEED_SERIAL) $(COM_OPTS)
endif

# We need to make sure SMING_HOME and ESP_HOME variables are set correctly.
# Set these above or use enviromental variables to set globally.

ifeq ("$(wildcard $(ESP_HOME)/sdk/Makefile)","")
$(error ESP SDK Makefile not found in $(ESP_HOME)/sdk. Please check that ESP_HOME is set to correct value)
endif

# Include main Sming Makefile
ifeq ($(RBOOT_ENABLED), 1)
ifeq ("$(wildcard $(SMING_HOME)/Makefile-rboot.mk)","")
$(error Sming Makefile not found in $(SMING_HOME). Please check that SMING_HOME is set to correct value)
endif
include $(SMING_HOME)/Makefile-rboot.mk
else
ifeq ("$(wildcard $(SMING_HOME)/Makefile-project.mk)","")
$(error Sming Makefile not found in $(SMING_HOME). Please check that SMING_HOME is set to correct value)
endif
include $(SMING_HOME)/Makefile-project.mk
endif

# Friendly names for targets (useful to display in IDE)
build: all
upload: flash
