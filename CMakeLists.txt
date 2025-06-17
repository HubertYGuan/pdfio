cmake_minimum_required(VERSION 3.0)
project(pdfio)

file(GLOB libsources pdf*.c ttf.c)

list(REMOVE_ITEM libsources *testpdfio.c *testttf.c)

set(warnings -Wall -Wunused -Wno-char-subscripts -Wno-format-truncation -Wno-format-y2k -Wno-switch -Wno-unused-result)
set(optim -g -Os)
set(cppflags -I/usr/include/libpng16  -DHAVE_LIBPNG=1  -DHAVE_TM_GMTOFF=1 -DHAVE_TIMEGM=1  -D_FORTIFY_SOURCE=2 -D__USE_MISC -D_GNU_SOURCE -D_TIME_BITS=64 -D_FILE_OFFSET_BITS=64)
set(cflags -fPIC  ${cppflags} ${optim} ${warnings})
set(libs -lpng16  -lz -lz   -lm)

add_library(pdfio STATIC ${libsources})

add_compile_options( ${cflags} )
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -H")
add_link_options( ${LIBS} )

set(CMAKE_AR /usr/bin/ar)
set(CMAKE_C_ARCHIVE_CREATE "<CMAKE_AR> cr <TARGET> <OBJECTS>")