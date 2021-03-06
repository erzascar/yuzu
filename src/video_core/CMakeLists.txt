add_library(video_core STATIC
    dma_pusher.cpp
    dma_pusher.h
    debug_utils/debug_utils.cpp
    debug_utils/debug_utils.h
    engines/fermi_2d.cpp
    engines/fermi_2d.h
    engines/kepler_compute.cpp
    engines/kepler_compute.h
    engines/kepler_memory.cpp
    engines/kepler_memory.h
    engines/maxwell_3d.cpp
    engines/maxwell_3d.h
    engines/maxwell_dma.cpp
    engines/maxwell_dma.h
    engines/shader_bytecode.h
    engines/shader_header.h
    gpu.cpp
    gpu.h
    gpu_asynch.cpp
    gpu_asynch.h
    gpu_synch.cpp
    gpu_synch.h
    gpu_thread.cpp
    gpu_thread.h
    macro_interpreter.cpp
    macro_interpreter.h
    memory_manager.cpp
    memory_manager.h
    morton.cpp
    morton.h
    rasterizer_cache.cpp
    rasterizer_cache.h
    rasterizer_interface.h
    renderer_base.cpp
    renderer_base.h
    renderer_opengl/gl_buffer_cache.cpp
    renderer_opengl/gl_buffer_cache.h
    renderer_opengl/gl_global_cache.cpp
    renderer_opengl/gl_global_cache.h
    renderer_opengl/gl_primitive_assembler.cpp
    renderer_opengl/gl_primitive_assembler.h
    renderer_opengl/gl_rasterizer.cpp
    renderer_opengl/gl_rasterizer.h
    renderer_opengl/gl_rasterizer_cache.cpp
    renderer_opengl/gl_rasterizer_cache.h
    renderer_opengl/gl_resource_manager.cpp
    renderer_opengl/gl_resource_manager.h
    renderer_opengl/gl_sampler_cache.cpp
    renderer_opengl/gl_sampler_cache.h
    renderer_opengl/gl_shader_cache.cpp
    renderer_opengl/gl_shader_cache.h
    renderer_opengl/gl_shader_decompiler.cpp
    renderer_opengl/gl_shader_decompiler.h
    renderer_opengl/gl_shader_disk_cache.cpp
    renderer_opengl/gl_shader_disk_cache.h
    renderer_opengl/gl_shader_gen.cpp
    renderer_opengl/gl_shader_gen.h
    renderer_opengl/gl_shader_manager.cpp
    renderer_opengl/gl_shader_manager.h
    renderer_opengl/gl_shader_util.cpp
    renderer_opengl/gl_shader_util.h
    renderer_opengl/gl_state.cpp
    renderer_opengl/gl_state.h
    renderer_opengl/gl_stream_buffer.cpp
    renderer_opengl/gl_stream_buffer.h
    renderer_opengl/maxwell_to_gl.h
    renderer_opengl/renderer_opengl.cpp
    renderer_opengl/renderer_opengl.h
    renderer_opengl/utils.cpp
    renderer_opengl/utils.h
    sampler_cache.cpp
    sampler_cache.h
    shader/decode/arithmetic.cpp
    shader/decode/arithmetic_immediate.cpp
    shader/decode/bfe.cpp
    shader/decode/bfi.cpp
    shader/decode/shift.cpp
    shader/decode/arithmetic_integer.cpp
    shader/decode/arithmetic_integer_immediate.cpp
    shader/decode/arithmetic_half.cpp
    shader/decode/arithmetic_half_immediate.cpp
    shader/decode/ffma.cpp
    shader/decode/hfma2.cpp
    shader/decode/conversion.cpp
    shader/decode/memory.cpp
    shader/decode/texture.cpp
    shader/decode/float_set_predicate.cpp
    shader/decode/integer_set_predicate.cpp
    shader/decode/half_set_predicate.cpp
    shader/decode/predicate_set_register.cpp
    shader/decode/predicate_set_predicate.cpp
    shader/decode/register_set_predicate.cpp
    shader/decode/float_set.cpp
    shader/decode/integer_set.cpp
    shader/decode/half_set.cpp
    shader/decode/video.cpp
    shader/decode/xmad.cpp
    shader/decode/other.cpp
    shader/decode.cpp
    shader/shader_ir.cpp
    shader/shader_ir.h
    shader/track.cpp
    surface.cpp
    surface.h
    textures/astc.cpp
    textures/astc.h
    textures/convert.cpp
    textures/convert.h
    textures/decoders.cpp
    textures/decoders.h
    textures/texture.h
    texture_cache.cpp
    texture_cache.h
    video_core.cpp
    video_core.h
)

if (ENABLE_VULKAN)
    target_sources(video_core PRIVATE
        renderer_vulkan/declarations.h
        renderer_vulkan/maxwell_to_vk.cpp
        renderer_vulkan/maxwell_to_vk.h
        renderer_vulkan/vk_buffer_cache.cpp
        renderer_vulkan/vk_buffer_cache.h
        renderer_vulkan/vk_device.cpp
        renderer_vulkan/vk_device.h
        renderer_vulkan/vk_memory_manager.cpp
        renderer_vulkan/vk_memory_manager.h
        renderer_vulkan/vk_resource_manager.cpp
        renderer_vulkan/vk_resource_manager.h
        renderer_vulkan/vk_sampler_cache.cpp
        renderer_vulkan/vk_sampler_cache.h
        renderer_vulkan/vk_scheduler.cpp
        renderer_vulkan/vk_scheduler.h
        renderer_vulkan/vk_shader_decompiler.cpp
        renderer_vulkan/vk_shader_decompiler.h
        renderer_vulkan/vk_stream_buffer.cpp
        renderer_vulkan/vk_stream_buffer.h
        renderer_vulkan/vk_swapchain.cpp
        renderer_vulkan/vk_swapchain.h)

    target_include_directories(video_core PRIVATE sirit ../../externals/Vulkan-Headers/include)
    target_compile_definitions(video_core PRIVATE HAS_VULKAN)
endif()

create_target_directory_groups(video_core)

target_link_libraries(video_core PUBLIC common core)
target_link_libraries(video_core PRIVATE glad)
if (ENABLE_VULKAN)
    target_link_libraries(video_core PRIVATE sirit)
endif()
