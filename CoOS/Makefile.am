# CoOS Makefile.am

lib_LTLIBRARIES = libcoos.la

sources = \
	portable/GCC/port.c \
	kernel/core.c \
	kernel/event.c \
	kernel/flag.c \
	kernel/hook.c \
	kernel/kernelHeap.c \
	kernel/mbox.c \
	kernel/mm.c \
	kernel/mutex.c \
	kernel/queue.c \
	kernel/sem.c \
	kernel/serviceReq.c \
	kernel/task.c \
	kernel/time.c \
	kernel/timer.c \
	kernel/utility.c

libcoos_la_CFLAGS = -Wno-missing-braces -Wno-missing-field-initializers -Wno-sign-compare
libcoos_la_SOURCES = $(sources)

