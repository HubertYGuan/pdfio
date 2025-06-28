if(CONFIG_PDFIO)
cmake_minimum_required(VERSION 3.20)
project(pdfio)

file(GLOB libsources pdf*.c ttf.c)

list(REMOVE_ITEM libsources *testpdfio.c *testttf.c)

set(warnings -Wall -Wunused -Wno-char-subscripts -Wno-format-truncation -Wno-format-y2k -Wno-switch -Wno-unused-result)
set(optim -g -Os)
set(cppflags -I/usr/include/libpng16  -DHAVE_LIBPNG=1  -DHAVE_TM_GMTOFF=1 -DHAVE_TIMEGM=1  -D_FORTIFY_SOURCE=2 -D__USE_MISC -D_GNU_SOURCE -D_TIME_BITS=64 -D_FILE_OFFSET_BITS=64)
set(cflags -fPIC  ${cppflags} ${optim} ${warnings})
set(libs -lpng16  -lz -lz   -lm)


zephyr_interface_library_named(PDFIO)

zephyr_include_directories(.)

zephyr_library()
zephyr_library_sources( ${libsources} )

zephyr_library_compile_options_ifdef(PDFIO_BUILD ${cflags})

zephyr_library_link_libraries(PDFIO)
target_link_libraries(PDFIO INTERFACE zephyr_interface)
endif(CONFIG_PDFIO)