CHECK_LIST := clock_without_librt
CHECK_LIST += cc_has_mfentry
CHECK_LIST += cxa_demangle
CHECK_LIST += have_libelf
CHECK_LIST += cc_has_mno_sse2
CHECK_LIST += have_libpython2.7
CHECK_LIST += perf_clockid
CHECK_LIST += perf_context_switch
CHECK_LIST += arm_has_hardfp
CHECK_LIST += have_libncurses

#
# This is needed for checking build dependency
#

CHECK_CFLAGS  = $(CFLAGS)  $(CFLAGS_$@)
CHECK_LDFLAGS = $(LDFLAGS) $(LDFLAGS_$@)

CFLAGS_cc_has_mfentry = -mfentry
LDFLAGS_cxa_demangle = -lstdc++
LDFLAGS_have_libelf = -lelf
CFLAGS_cc_has_mno_sse2 = -mno-sse2
LDFLAGS_have_libpython2.7 = -lpython2.7
CFLAGS_have_libncurses = $(shell pkg-config --cflags ncursesw)
LDFLAGS_have_libncurses = $(shell pkg-config --libs ncursesw)

check-build: check-tstamp $(CHECK_LIST)

$(CHECK_LIST): %: __%.c
	@$(CC) $(CHECK_CFLAGS) -o $@ $< $(CHECK_LDFLAGS) > /dev/null 2>&1

check-tstamp: PHONY
	@touch $@
	@if [ `id -u` -eq 0 ]; then chmod 666 $@; fi

check-clean:
	@$(RM) $(shell find -type f -executable) check-tstamp *.o

.PHONY: PHONY;
