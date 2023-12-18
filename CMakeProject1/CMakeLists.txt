# CMakeList.txt : CMakeProject1 の CMake プロジェクト。ソースを含めて、次を定義します:
# プロジェクト専用ロジックはこちらです。

# SDL2のパスを設定
set(SDL2_DIR "C:\\sdl2\\cmake")

# SDL2を探す
find_package(SDL2 REQUIRED)

# make an imgui folder and put all of these files in the imgui folder
set(IMGUI_SRC
        imgui/imgui_impl_opengl3.h
        imgui/imgui_impl_opengl3.cpp
        imgui/imgui_impl_opengl3_loader.h
        imgui/imgui_impl_sdl2.h
        imgui/imgui_impl_sdl2.cpp
        imgui/imgui.h
        imgui/imgui.cpp
        imgui/imgui_draw.cpp
        imgui/imgui_tables.cpp
        imgui/imgui_widgets.cpp
        imgui/imgui_demo.cpp
        )

# インクルードディレクトリを追加
include_directories(${SDL2_INCLUDE_DIRS})

# ソースをこのプロジェクトの実行可能ファイルに追加します。
add_executable(CMakeProject1 "CMakeProject1.cpp" "CMakeProject1.h" ${IMGUI_SRC})

# ターゲットにSDL2ライブラリをリンク
target_link_libraries(CMakeProject1 PRIVATE ${SDL2_LIBRARIES} opengl32)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET CMakeProject1 PROPERTY CXX_STANDARD 20)
endif()

# Windows向けのビルド構成
if (WIN32)
  # Windows向けの追加の設定
  # SDL2mainのリンクを行わない
  #target_link_libraries(CMakeProject1 PRIVATE SDL2main)
endif()

# Linux向けのビルド構成
if (UNIX AND NOT APPLE)
  # Linux向けの追加の設定
  target_link_libraries(CMakeProject1 PRIVATE m)
endif()

# macOS向けのビルド構成
if (APPLE)
  # macOS向けの追加の設定
  target_link_libraries(CMakeProject1 PRIVATE "-framework Cocoa" "-framework OpenGL" "-framework IOKit" "-framework CoreVideo")
endif()

# TODO: テストを追加し、必要な場合は、ターゲットをインストールします。
