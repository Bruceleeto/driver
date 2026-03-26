DEBUG ?= 0
GAME_REGION ?= NTSC_VERSION

CC = gcc
CXX = g++
AR = ar

COMMON_WARNS = -Wno-narrowing -Wno-endif-labels -Wno-write-strings -Wno-format-security -Wno-unused-result
CFLAGS = -m32 $(COMMON_WARNS) -fpermissive
CXXFLAGS = -m32 -std=c++11 $(COMMON_WARNS) -fpermissive
LDFLAGS = -m32

ifeq ($(DEBUG), 1)
  CFLAGS += -g -D_DEBUG -DDEBUG -DDEBUG_OPTIONS -DCOLLISION_DEBUG -DCUTSCENE_RECORDER
  CXXFLAGS += -g -D_DEBUG -DDEBUG -DDEBUG_OPTIONS -DCOLLISION_DEBUG -DCUTSCENE_RECORDER
  BINDIR = bin/Debug
  OBJDIR = obj/Debug
  SUFFIX = _dbg
  BUILD_CFG = Debug
else
  CFLAGS += -O3 -DNDEBUG
  CXXFLAGS += -O3 -DNDEBUG
  LDFLAGS += -s
  BINDIR = bin/Release
  OBJDIR = obj/Release
  SUFFIX =
  BUILD_CFG = Release
endif

CFLAGS += -D$(GAME_REGION) -DBUILD_CONFIGURATION_STRING=\"$(BUILD_CFG)\"
CXXFLAGS += -D$(GAME_REGION) -DBUILD_CONFIGURATION_STRING=\"$(BUILD_CFG)\"

# Directories
PSYCROSS_SRCDIR = PsyCross/src
GAME_SRCDIR = Game
UTILS_SRCDIR = utils

# Include paths
PSYCROSS_INCLUDES = -IPsyCross/include -IPsyCross/include/psx -I/usr/include/SDL2
REDRIVER2_INCLUDES = -IGame -IPsyCross/include -IPsyCross/include/psx -I/usr/include/SDL2

# Output
PSYCROSS_LIB = $(BINDIR)/libPsyCross.a
REDRIVER2_EXE = $(BINDIR)/REDRIVER2$(SUFFIX)

PSYCROSS_OBJDIR = $(OBJDIR)/PsyCross
REDRIVER2_OBJDIR = $(OBJDIR)/REDRIVER2

# --- PsyCross objects ---
PSYCROSS_OBJS = \
	$(PSYCROSS_OBJDIR)/PsyX_main.o \
	$(PSYCROSS_OBJDIR)/PsyX_GPU.o \
	$(PSYCROSS_OBJDIR)/PsyX_GTE.o \
	$(PSYCROSS_OBJDIR)/PsyX_SPUAL.o \
	$(PSYCROSS_OBJDIR)/half_float.o \
	$(PSYCROSS_OBJDIR)/PsyX_pad.o \
	$(PSYCROSS_OBJDIR)/PsyX_render.o \
	$(PSYCROSS_OBJDIR)/crash_handler.o \
	$(PSYCROSS_OBJDIR)/ABS.o \
	$(PSYCROSS_OBJDIR)/INLINE_C.o \
	$(PSYCROSS_OBJDIR)/LIBAPI.o \
	$(PSYCROSS_OBJDIR)/LIBCD.o \
	$(PSYCROSS_OBJDIR)/LIBETC.o \
	$(PSYCROSS_OBJDIR)/LIBGPU.o \
	$(PSYCROSS_OBJDIR)/LIBGTE.o \
	$(PSYCROSS_OBJDIR)/LIBMCRD.o \
	$(PSYCROSS_OBJDIR)/LIBPAD.o \
	$(PSYCROSS_OBJDIR)/LIBSN.o \
	$(PSYCROSS_OBJDIR)/LIBSPU.o \
	$(PSYCROSS_OBJDIR)/glad.o \
	$(PSYCROSS_OBJDIR)/timer.o

# --- REDRIVER2 objects ---
# Game/ASM
REDRIVER2_OBJS = \
	$(REDRIVER2_OBJDIR)/asmtest.o \
	$(REDRIVER2_OBJDIR)/compres.o \
	$(REDRIVER2_OBJDIR)/d2mapasm.o \
	$(REDRIVER2_OBJDIR)/rnc_2.o \
	$(REDRIVER2_OBJDIR)/rndrasm.o

# Game/C
REDRIVER2_OBJS += \
	$(REDRIVER2_OBJDIR)/ai.o \
	$(REDRIVER2_OBJDIR)/bcoll3d.o \
	$(REDRIVER2_OBJDIR)/bcollide.o \
	$(REDRIVER2_OBJDIR)/bomberman.o \
	$(REDRIVER2_OBJDIR)/camera.o \
	$(REDRIVER2_OBJDIR)/cars.o \
	$(REDRIVER2_OBJDIR)/cell.o \
	$(REDRIVER2_OBJDIR)/civ_ai.o \
	$(REDRIVER2_OBJDIR)/convert.o \
	$(REDRIVER2_OBJDIR)/cop_ai.o \
	$(REDRIVER2_OBJDIR)/cosmetic.o \
	$(REDRIVER2_OBJDIR)/cutrecorder.o \
	$(REDRIVER2_OBJDIR)/cutscene.o \
	$(REDRIVER2_OBJDIR)/debris.o \
	$(REDRIVER2_OBJDIR)/denting.o \
	$(REDRIVER2_OBJDIR)/director.o \
	$(REDRIVER2_OBJDIR)/dr2roads.o \
	$(REDRIVER2_OBJDIR)/draw.o \
	$(REDRIVER2_OBJDIR)/drivinggames.o \
	$(REDRIVER2_OBJDIR)/E3stuff.o \
	$(REDRIVER2_OBJDIR)/envsound.o \
	$(REDRIVER2_OBJDIR)/event.o \
	$(REDRIVER2_OBJDIR)/felony.o \
	$(REDRIVER2_OBJDIR)/fmvplay.o \
	$(REDRIVER2_OBJDIR)/gamesnd.o \
	$(REDRIVER2_OBJDIR)/glaunch.o \
	$(REDRIVER2_OBJDIR)/handling.o \
	$(REDRIVER2_OBJDIR)/job_fx.o \
	$(REDRIVER2_OBJDIR)/leadai.o \
	$(REDRIVER2_OBJDIR)/loadsave.o \
	$(REDRIVER2_OBJDIR)/loadview.o \
	$(REDRIVER2_OBJDIR)/main.o \
	$(REDRIVER2_OBJDIR)/map.o \
	$(REDRIVER2_OBJDIR)/mc_snd.o \
	$(REDRIVER2_OBJDIR)/mdraw.o \
	$(REDRIVER2_OBJDIR)/mgeneric.o \
	$(REDRIVER2_OBJDIR)/mission.o \
	$(REDRIVER2_OBJDIR)/models.o \
	$(REDRIVER2_OBJDIR)/motion_c.o \
	$(REDRIVER2_OBJDIR)/objanim.o \
	$(REDRIVER2_OBJDIR)/objcoll.o \
	$(REDRIVER2_OBJDIR)/overlay.o \
	$(REDRIVER2_OBJDIR)/overmap.o \
	$(REDRIVER2_OBJDIR)/pad.o \
	$(REDRIVER2_OBJDIR)/pathfind.o \
	$(REDRIVER2_OBJDIR)/pause.o \
	$(REDRIVER2_OBJDIR)/pedest.o \
	$(REDRIVER2_OBJDIR)/players.o \
	$(REDRIVER2_OBJDIR)/pres.o \
	$(REDRIVER2_OBJDIR)/replays.o \
	$(REDRIVER2_OBJDIR)/roadbits.o \
	$(REDRIVER2_OBJDIR)/scores.o \
	$(REDRIVER2_OBJDIR)/search.o \
	$(REDRIVER2_OBJDIR)/shadow.o \
	$(REDRIVER2_OBJDIR)/sky.o \
	$(REDRIVER2_OBJDIR)/sound.o \
	$(REDRIVER2_OBJDIR)/spool.o \
	$(REDRIVER2_OBJDIR)/state.o \
	$(REDRIVER2_OBJDIR)/sysclock.o \
	$(REDRIVER2_OBJDIR)/system.o \
	$(REDRIVER2_OBJDIR)/targets.o \
	$(REDRIVER2_OBJDIR)/texture.o \
	$(REDRIVER2_OBJDIR)/tile.o \
	$(REDRIVER2_OBJDIR)/time.o \
	$(REDRIVER2_OBJDIR)/wheelforces.o \
	$(REDRIVER2_OBJDIR)/xaplay.o \
	$(REDRIVER2_OBJDIR)/xmplay.o

# Game/Frontend
REDRIVER2_OBJS += \
	$(REDRIVER2_OBJDIR)/FEmain.o

# Game root
REDRIVER2_OBJS += \
	$(REDRIVER2_OBJDIR)/dr2locale.o

# utils
REDRIVER2_OBJS += \
	$(REDRIVER2_OBJDIR)/DebugOverlay.o \
	$(REDRIVER2_OBJDIR)/fs.o \
	$(REDRIVER2_OBJDIR)/ini.o \
	$(REDRIVER2_OBJDIR)/riff.o \
	$(REDRIVER2_OBJDIR)/targa.o \
	$(REDRIVER2_OBJDIR)/snd_al_source.o \
	$(REDRIVER2_OBJDIR)/snd_wav_cache.o \
	$(REDRIVER2_OBJDIR)/snd_wav_source.o \
	$(REDRIVER2_OBJDIR)/ReadAVI.o \
	$(REDRIVER2_OBJDIR)/VideoPlayer.o

# top-level
REDRIVER2_OBJS += \
	$(REDRIVER2_OBJDIR)/redriver2_psxpc.o

REDRIVER2_LIBS = -ljpeg -lGL -lopenal -lSDL2 

# =============================================================
.PHONY: all clean help

all: $(REDRIVER2_EXE)

$(REDRIVER2_EXE): $(PSYCROSS_LIB) $(REDRIVER2_OBJS)
	@mkdir -p $(BINDIR)
	@echo "Linking REDRIVER2"
	$(CXX) $(LDFLAGS) -o $@ $(REDRIVER2_OBJS) $(PSYCROSS_LIB) $(REDRIVER2_LIBS)

$(PSYCROSS_LIB): $(PSYCROSS_OBJS)
	@mkdir -p $(BINDIR)
	@echo "Creating PsyCross library"
	$(AR) rcs $@ $(PSYCROSS_OBJS)

# --- PsyCross compile rules ---

$(PSYCROSS_OBJDIR)/PsyX_main.o: $(PSYCROSS_SRCDIR)/PsyX_main.cpp
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CXX) $(CXXFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

$(PSYCROSS_OBJDIR)/PsyX_GPU.o: $(PSYCROSS_SRCDIR)/gpu/PsyX_GPU.cpp
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CXX) $(CXXFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

$(PSYCROSS_OBJDIR)/PsyX_GTE.o: $(PSYCROSS_SRCDIR)/gte/PsyX_GTE.cpp
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CXX) $(CXXFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

$(PSYCROSS_OBJDIR)/half_float.o: $(PSYCROSS_SRCDIR)/gte/half_float.cpp
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CXX) $(CXXFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

$(PSYCROSS_OBJDIR)/PsyX_SPUAL.o: $(PSYCROSS_SRCDIR)/audio/PsyX_SPUAL.cpp
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CXX) $(CXXFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

$(PSYCROSS_OBJDIR)/PsyX_pad.o: $(PSYCROSS_SRCDIR)/pad/PsyX_pad.cpp
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CXX) $(CXXFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

$(PSYCROSS_OBJDIR)/PsyX_render.o: $(PSYCROSS_SRCDIR)/render/PsyX_render.cpp
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CXX) $(CXXFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

$(PSYCROSS_OBJDIR)/crash_handler.o: $(PSYCROSS_SRCDIR)/util/crash_handler.cpp
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CXX) $(CXXFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

$(PSYCROSS_OBJDIR)/glad.o: $(PSYCROSS_SRCDIR)/render/glad.c
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CC) $(CFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

$(PSYCROSS_OBJDIR)/timer.o: $(PSYCROSS_SRCDIR)/util/timer.c
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CC) $(CFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

# PsyCross .C files (PSX stubs)
$(PSYCROSS_OBJDIR)/%.o: $(PSYCROSS_SRCDIR)/psx/%.C
	@mkdir -p $(PSYCROSS_OBJDIR)
	$(CXX) $(CXXFLAGS) $(PSYCROSS_INCLUDES) -c $< -o $@

# --- REDRIVER2 compile rules ---
# All .c files compiled as C++

$(REDRIVER2_OBJDIR)/%.o: $(GAME_SRCDIR)/ASM/%.c
	@mkdir -p $(REDRIVER2_OBJDIR)
	$(CXX) $(CFLAGS) -x c++ $(REDRIVER2_INCLUDES) -c $< -o $@

$(REDRIVER2_OBJDIR)/%.o: $(GAME_SRCDIR)/C/%.c
	@mkdir -p $(REDRIVER2_OBJDIR)
	$(CXX) $(CFLAGS) -x c++ $(REDRIVER2_INCLUDES) -c $< -o $@

$(REDRIVER2_OBJDIR)/FEmain.o: $(GAME_SRCDIR)/Frontend/FEmain.c
	@mkdir -p $(REDRIVER2_OBJDIR)
	$(CXX) $(CFLAGS) -x c++ $(REDRIVER2_INCLUDES) -c $< -o $@

$(REDRIVER2_OBJDIR)/dr2locale.o: $(GAME_SRCDIR)/dr2locale.c
	@mkdir -p $(REDRIVER2_OBJDIR)
	$(CXX) $(CFLAGS) -x c++ $(REDRIVER2_INCLUDES) -c $< -o $@

$(REDRIVER2_OBJDIR)/%.o: $(UTILS_SRCDIR)/%.cpp
	@mkdir -p $(REDRIVER2_OBJDIR)
	$(CXX) $(CXXFLAGS) $(REDRIVER2_INCLUDES) -c $< -o $@

$(REDRIVER2_OBJDIR)/ini.o: $(UTILS_SRCDIR)/ini.c
	@mkdir -p $(REDRIVER2_OBJDIR)
	$(CXX) $(CFLAGS) -x c++ $(REDRIVER2_INCLUDES) -c $< -o $@

$(REDRIVER2_OBJDIR)/%.o: $(UTILS_SRCDIR)/audio_source/%.cpp
	@mkdir -p $(REDRIVER2_OBJDIR)
	$(CXX) $(CXXFLAGS) $(REDRIVER2_INCLUDES) -c $< -o $@

$(REDRIVER2_OBJDIR)/%.o: $(UTILS_SRCDIR)/video_source/%.cpp
	@mkdir -p $(REDRIVER2_OBJDIR)
	$(CXX) $(CXXFLAGS) $(REDRIVER2_INCLUDES) -c $< -o $@

$(REDRIVER2_OBJDIR)/redriver2_psxpc.o: redriver2_psxpc.cpp
	@mkdir -p $(REDRIVER2_OBJDIR)
	$(CXX) $(CXXFLAGS) $(REDRIVER2_INCLUDES) -c $< -o $@

clean:
	rm -rf obj bin

help:
	@echo "Usage: make [DEBUG=1] [GAME_REGION=PAL_VERSION] [target]"
	@echo ""
	@echo "Targets:"
	@echo "  all     - Build everything (default)"
	@echo "  clean   - Remove all built files"
	@echo "  help    - Show this help"
	@echo ""
	@echo "Options:"
	@echo "  DEBUG=1              - Build with debug symbols"
	@echo "  DEBUG=0              - Build optimized release (default)"
	@echo "  GAME_REGION=X        - NTSC_VERSION (default) or PAL_VERSION"
