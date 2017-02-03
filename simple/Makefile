CC		 = $(CROSS_COMPILE)gcc
AR		 = $(CROSS_COMPILE)ar
RM		 = rm -rf
ECHO	 = echo -e
MKDIR	 = mkdir -p
ifneq ($(V),)
Q		 =
else
Q		 = @
endif

TARGET		?= my_app
OBJ_DIR		?= .obj

SRCS		:=
SRCS		+= main.c
SRCS		+= util.c
SRCS		+= output.c

OBJS		 = $(foreach src, $(SRCS), $(OBJ_DIR)/$(src:.c=.o))

CFLAGS		+= -O2 -g
CFLAGS		+= -Wall -Wno-unused-function

LDFLAGS		+= -lpthread

all: $(TARGET)

$(TARGET):$(OBJS)
	@$(ECHO) "Linking... $(notdir $@)"
	$(Q)$(CC) -o $@ $(OBJS) $(LDFLAGS)

$(OBJ_DIR)/%.o: %.c Makefile
	@$(MKDIR) $(dir $@)
	@$(ECHO)  "Compile... $(notdir $@)"
	$(Q)$(CC) -MD $(CFLAGS) -c $< -o $@

clean \
distclean:
	$(Q)$(RM) $(OBJ_DIR) $(TARGET)

ifeq ($(filter clean distclean,$(MAKECMDGOALS)),)
-include $(OBJS:.o=.d)
endif
