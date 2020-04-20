SRCDIR=./source
SRC= \
	$(SRCDIR)/convolve.c \
	$(SRCDIR)/decimate.c \
	$(SRCDIR)/math_utils.c \
	$(SRCDIR)/mse.c \
	$(SRCDIR)/psnr.c \
	$(SRCDIR)/ssim.c \
	$(SRCDIR)/ms_ssim.c

OBJ = $(SRC:.c=.o)

INCLUDES = -I./include
CC ?= gcc

ifeq ($(RELEASE),1)
OUTDIR=./build/release
CFLAGS= -Wall -O3 -pipe -march=native -flto -D_FORTIFY_SOURCE=2 -fPIC -fstack-protector-all
else
OUTDIR=./build/debug
CFLAGS=-g -Wall
endif

OUT = $(OUTDIR)/libiqa.a

.c.o:
	$(CC) $(INCLUDES) $(CFLAGS) -c $< -o $@

$(OUT): $(OBJ)
	mkdir -p $(OUTDIR)
	ar rcs $(OUT) $(OBJ)
	mv $(OBJ) $(OUTDIR)

clean:
	rm -f $(OUTDIR)/*.o $(OUT) $(SRCDIR)/*.o
	cd test; $(MAKE) clean;

.PHONY : test
test:
	cd test; $(MAKE);
