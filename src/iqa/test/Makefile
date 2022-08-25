SRCDIR=./source
SRC= \
	$(SRCDIR)/bmp.c \
	$(SRCDIR)/hptime.c \
	$(SRCDIR)/main.c \
	$(SRCDIR)/test_convolve.c \
	$(SRCDIR)/test_decimate.c \
	$(SRCDIR)/test_mse.c \
	$(SRCDIR)/test_psnr.c \
	$(SRCDIR)/test_ssim.c \
	$(SRCDIR)/test_ms_ssim.c

OBJ = $(SRC:.c=.o)

INCLUDES = -I./include -I../include
CC ?= icc

ifeq ($(RELEASE),1)
OUTDIR=../build/release
CFLAGS= -Wall -O3 -pipe -xHost -static-intel -flto -D_FORTIFY_SOURCE=2 -fPIC -pie -fstack-protector-all

else
OUTDIR=../build/debug
CFLAGS += -O0 -g -Wall
endif

OUT = $(OUTDIR)/test

LFLAGS=-L$(OUTDIR) -static-intel
LIBS=$(OUTDIR)/libiqa.a -lm -lrt

.c.o:
	$(CC) $(INCLUDES) $(CFLAGS) -c $< -o $@

$(OUT): $(OBJ)
	mkdir -p $(OUTDIR)
	$(CC) $(INCLUDES) $(CFLAGS) $(LFLAGS) $^ $(LIBS) -o $@
	cp ./resources/*.bmp $(OUTDIR)
	mv $(OBJ) $(OUTDIR)

clean:
	rm -f $(OUTDIR)/*.o $(OUT) $(SRCDIR)/*.o
	rm -f $(OUTDIR)/*.bmp

