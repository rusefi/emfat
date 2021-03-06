##############################################################################
# Build global options
# NOTE: Can be overridden externally.
#

PROJECT_DIR = .

# by default EXTRA_PARAMS is empty and we create 'debug' version of the firmware with additional assertions and statistics
# for 'release' options see 'clean_compile_two_versions.bat' file


# Compiler options here.
ifeq ($(USE_OPT),)
#  USE_OPT = -O2 -ggdb -std=gnu99 -fomit-frame-pointer -falign-functions=16
#  USE_OPT = $(RFLAGS) -O1 -fgnu89-inline -ggdb -fomit-frame-pointer -falign-functions=16 -std=gnu99 -Werror-implicit-function-declaration -Werror -Wno-error=pointer-sign -Wno-error=unused-function -Wno-error=unused-variable -Wno-error=sign-compare -Wno-error=unused-parameter -Wno-error=missing-field-initializers
  USE_OPT = $(EXTRA_PARAMS) $(RFLAGS) -O2        -fomit-frame-pointer -falign-functions=16 -Werror-implicit-function-declaration -Werror -Wno-error=pointer-sign -Wno-error=unused-function -Wno-error=unused-variable -Wno-error=sign-compare -Wno-error=unused-parameter -Wno-error=missing-field-initializers -Werror=type-limits -Wno-error=strict-aliasing -Wno-error=attributes -Wno-error=aggressive-loop-optimizations -Wno-error=parentheses
endif

# C specific options here (added to USE_OPT).
ifeq ($(USE_COPT),)
  USE_COPT = -fgnu89-inline -std=gnu99
endif

# C++ specific options here (added to USE_OPT).
ifeq ($(USE_CPPOPT),)
  USE_CPPOPT = -std=c++11 -fno-rtti -fno-exceptions -fno-use-cxa-atexit -Werror=write-strings -Werror=type-limits
endif

# Enable this if you want the linker to remove unused code and data
ifeq ($(USE_LINK_GC),)
  USE_LINK_GC = yes
endif

# Linker extra options here.
ifeq ($(USE_LDOPT),)
  USE_LDOPT = 
endif

# Enable this if you want link time optimizations (LTO)
ifeq ($(USE_LTO),)
  USE_LTO = no
endif

# If enabled, this option allows to compile the application in THUMB mode.
ifeq ($(USE_THUMB),)
  USE_THUMB = yes
endif

# Enable this if you want to see the full log while compiling.
ifeq ($(USE_VERBOSE_COMPILE),)
  USE_VERBOSE_COMPILE = no
endif

#
# Build global options
##############################################################################

##############################################################################
# Architecture or project specific options
#

USE_FPU = softfp

# Enables the use of FPU on Cortex-M4 (no, softfp, hard).
ifeq ($(USE_FPU),)
  USE_FPU = no
endif

#
# Architecture or project specific options
##############################################################################

##############################################################################
# Project, sources and paths
#

# Define project name here
PROJECT = rusefi

# Imported source files and paths
CHIBIOS = chibios
#include $(CHIBIOS)/test/test.mk

#PROJECT_BOARD = OLIMEX_STM32_E407
ifneq ($(PROJECT_BOARD),OLIMEX_STM32_E407)
  PROJECT_BOARD = ST_STM32F4_DISCOVERY
endif
DDEFS += -D$(PROJECT_BOARD) -DSTM32F40XX -DUSE_USB_OTG_FS -DCRT0_INIT_CORE=FALSE


# Imported source files and paths
include ../std-periph/src/periph.mk \
	../usb-files/usb-files.mk \
	../usb-files/msc-class/src/msc-class.mk \
	../usb-core/otg-driver/otg-driver.mk \
	../usb-core/dev-driver/dev-driver.mk


# Define linker script file here
LDSCRIPT= STM32F407xG_CCM.ld

# C sources that can be compiled in ARM or THUMB mode depending on the global
# setting.
CSRC =	$(PERIPH) \
	$(USB_FILES) \
	$(MSC_CLASS) \
	$(OTG_DRIVER) \
	$(DEV_DRIVER) \
	app.c \
	emfat.c \
	crt0.c \
	Interrupts.c \
	StorageMode.c
 

# C++ sources that can be compiled in ARM or THUMB mode depending on the global
# setting.
CPPSRC = 

# C sources to be compiled in ARM mode regardless of the global setting.
# NOTE: Mixing ARM and THUMB mode enables the -mthumb-interwork compiler
#       option that results in lower performance and larger code size.
ACSRC =

# C++ sources to be compiled in ARM mode regardless of the global setting.
# NOTE: Mixing ARM and THUMB mode enables the -mthumb-interwork compiler
#       option that results in lower performance and larger code size.
ACPPSRC =

# C sources to be compiled in THUMB mode regardless of the global setting.
# NOTE: Mixing ARM and THUMB mode enables the -mthumb-interwork compiler
#       option that results in lower performance and larger code size.
TCSRC =

# C sources to be compiled in THUMB mode regardless of the global setting.
# NOTE: Mixing ARM and THUMB mode enables the -mthumb-interwork compiler
#       option that results in lower performance and larger code size.
TCPPSRC =

# List ASM source files here
ASMSRC = crt0_v7m.s

INCDIR=	\
	../usb-files/msc-class/inc \
	../usb-core/dev-driver \
	../usb-core/otg-driver \
	../usb-files \
	../CMSIS \
	../std-periph\inc \
	.

#
# Project, sources and paths
##############################################################################

##############################################################################
# Compiler settings
#

MCU  = cortex-m4

#TRGT = arm-elf-
TRGT = arm-none-eabi-
CC   = $(TRGT)gcc
CPPC = $(TRGT)g++
# Enable loading with g++ only if you need C++ runtime support.
# NOTE: You can use C++ even without C++ support if you are careful. C++
#       runtime support makes code size explode.
LD   = $(TRGT)gcc
#LD   = $(TRGT)g++
CP   = $(TRGT)objcopy
AS   = $(TRGT)gcc -x assembler-with-cpp
OD   = $(TRGT)objdump
SZ   = $(TRGT)size
HEX  = $(CP) -O ihex
BIN  = $(CP) -O binary

# ARM-specific options here
AOPT =

# THUMB-specific options here
TOPT = -mthumb -DTHUMB

# Define C warning options here
CWARN = -Wall -Wextra -Wstrict-prototypes

# Define C++ warning options here
CPPWARN = -Wall -Wextra

#
# Compiler settings
##############################################################################

##############################################################################
# Start of default section
#

# List all default C defines here, like -D_DEBUG=1
# DDEFS =

# List all default ASM defines here, like -D_DEBUG=1
DADEFS =

# List all default directories to look for include files here
DINCDIR =

# List the default directory to look for the libraries here
DLIBDIR =

# List all default libraries here
DLIBS =

#
# End of default section
##############################################################################

##############################################################################
# Start of user section
#

# List all user C define here, like -D_DEBUG=1
UDEFS =

# Define ASM defines here
UADEFS =

# List all user directories here
UINCDIR =

# List the user directory to look for the libraries here
ULIBDIR =

# List all user libraries here
ULIBS = -lm

#
# End of user defines
##############################################################################

#RULESPATH = $(CHIBIOS)/os/ports/GCC/ARMCMx
RULESPATH = .
include $(RULESPATH)/rules.mk
