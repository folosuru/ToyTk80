
set(CMAKE_C_STANDARD 11)


add_executable(ToyZk80_emu
        main.c
        core.c
        display.c
        instruction.c
        instruction/logic_instruction.c
        instruction/ld_instruction.c
        instruction/math_instruction.c
        instruction/condition_instruction.c
        instruction/unimplement_instruction.c
        instruction/jump_instruction.c
        instruction/stack_instruction.c
        instruction/call_instruction.c
        # file_reader.c
)

if (WIN32)
        add_subdirectory(lib)
        target_link_libraries(ToyZk80_emu PRIVATE pdcurses)
else()
        find_package(Curses)
        target_link_libraries(ToyZk80_emu PRIVATE ${CURSES_LIBRARIES})
endif()





target_compile_options(ToyZk80_emu
        PRIVATE -masm=intel -O3
)
target_compile_definitions(ToyZk80_emu
        PRIVATE
        $<$<CONFIG:Debug>:DEBUG>
)
target_include_directories(ToyZk80_emu PRIVATE ../)
target_link_libraries(ToyZk80_emu PRIVATE ToyZk80_util ToyZk80_instruction)
