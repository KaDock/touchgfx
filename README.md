# docker-touchgfx
Container to build TouchGFX applications

## Prepare

    # As I don't know if I may distribute the zip, you need to get the trial yourself
    unzip -d touchgfx-4.6.1-eval touchgfx-4.6.1-eval.zip

    # As I can't change the touchgfx_path via ENV
    sed -i.bak 's;touchgfx_path := ../../../touchgfx;touchgfx_path := ../touchgfx;g' touchgfx-4.6.1-eval/app/example/clock_example/config/gcc/app.mk
    rm touchgfx-4.6.1-eval/app/example/clock_example/config/gcc/app.mk.bak

    # Exec bit
    chmod +x touchgfx-4.6.1-eval/touchgfx/framework/tools/fontconvert/build/linux/fontconvert.out
    chmod +x touchgfx-4.6.1-eval/touchgfx/framework/tools/imageconvert/build/linux/imageconvert.out

## OSX

XQuartz should be installed (via brew or other means - remember to relog)

    # In a terminal run this to enable X11Forward
    socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"

    # The IP may be another - its the one on your en1 (wifi) or en0 (eth)
    docker run -it --rm \
           --env=DISPLAY=10.192.0.179:0 \
           -v $(pwd)/touchgfx-4.6.1-eval/app/example/clock_example:/app:Z \
           -v $(pwd)/touchgfx-4.6.1-eval/touchgfx:/touchgfx:Z \
           kalledk/touchgfx \
           clean run
