cmake_minimum_required(VERSION 2.8)
Project(Demo2)
aux_source_directory(. DIR_SRCS)
add_executable(main ${DIR_SRCS})
