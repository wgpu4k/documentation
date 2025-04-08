# Getting Started with wgpu4k

Welcome to the wgpu4k documentation! wgpu4k is a Kotlin binding for WebGPU, providing a type-safe and idiomatic Kotlin API for GPU programming.

## What is wgpu4k?

wgpu4k is a Kotlin library that provides bindings to the WebGPU API, allowing you to write GPU-accelerated applications in Kotlin. It's designed to be:

- **Type-safe**: Leverages Kotlin's strong type system to catch errors at compile time
- **Idiomatic**: Follows Kotlin conventions and patterns
- **Efficient**: Provides high-performance access to GPU capabilities
- **Cross-platform**: Works on multiple platforms where WebGPU is supported

## Installation

### Gradle

Add the following to your `build.gradle.kts` file:

```kotlin
repositories {
    mavenCentral()
    // Add the repository where wgpu4k is hosted
    maven("https://jitpack.io")
}

dependencies {
    implementation("io.github.wgpu4k:wgpu4k:0.1.0") // Replace with the latest version
}
```

### Maven

Add the following to your `pom.xml` file:

```
<!-- Maven repository configuration -->
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>

<!-- Maven dependencies -->
<dependencies>
    <dependency>
        <groupId>io.github.wgpu4k</groupId>
        <artifactId>wgpu4k</artifactId>
        <version>0.1.0</version>
    </dependency>
</dependencies>
```

## Basic Usage

Here's a simple example to get you started with wgpu4k:

```kotlin
// Simple WebGPU example with wgpu4k
fun main() {
    // Initialize WebGPU
    val instance = Instance.create()

    // Request an adapter
    val adapter = instance.requestAdapter()

    // Create a device
    val device = adapter.requestDevice()

    // Create a shader module
    val shaderModule = device.createShaderModule("""
        @vertex
        fn vertexMain(@builtin(vertex_index) vertexIndex: u32) -> @builtin(position) vec4<f32> {
            var pos = array<vec2<f32>, 3>(
                vec2<f32>(0.0, 0.5),
                vec2<f32>(-0.5, -0.5),
                vec2<f32>(0.5, -0.5)
            );
            return vec4<f32>(pos[vertexIndex], 0.0, 1.0);
        }

        @fragment
        fn fragmentMain() -> @location(0) vec4<f32> {
            return vec4<f32>(1.0, 0.0, 0.0, 1.0);
        }
    """)

    // Create a render pipeline
    val pipeline = device.createRenderPipeline(
        RenderPipelineDescriptor(
            vertex = VertexState(
                module = shaderModule,
                entryPoint = "vertexMain"
            ),
            fragment = FragmentState(
                module = shaderModule,
                entryPoint = "fragmentMain",
                targets = listOf(
                    ColorTargetState(format = TextureFormat.BGRA8_UNORM)
                )
            ),
            primitive = PrimitiveState(topology = PrimitiveTopology.TRIANGLE_LIST)
        )
    )

    // ... Continue with rendering code
}
```

## Common Patterns

### Creating Buffers

```kotlin
// Create a vertex buffer
val vertices = floatArrayOf(
    0.0f, 0.5f,    // Vertex 1
    -0.5f, -0.5f,  // Vertex 2
    0.5f, -0.5f    // Vertex 3
)

val vertexBuffer = device.createBuffer(
    BufferDescriptor(
        size = vertices.size * Float.SIZE_BYTES,
        usage = BufferUsage.VERTEX.or(BufferUsage.COPY_DST)
    )
)

// Write data to the buffer
device.queue.writeBuffer(vertexBuffer, 0, vertices)
```

### Rendering a Frame

```kotlin
// Assuming you have a swapChain and commandEncoder set up
val textureView = swapChain.getCurrentTextureView()
val renderPass = commandEncoder.beginRenderPass(
    RenderPassDescriptor(
        colorAttachments = listOf(
            RenderPassColorAttachment(
                view = textureView,
                loadOp = LoadOp.CLEAR,
                storeOp = StoreOp.STORE,
                clearValue = Color(0.1f, 0.2f, 0.3f, 1.0f)
            )
        )
    )
)

renderPass.setPipeline(pipeline)
renderPass.draw(3, 1, 0, 0)
renderPass.end()

val commandBuffer = commandEncoder.finish()
device.queue.submit(listOf(commandBuffer))
```

### Compute Shaders

```kotlin
// Create a compute shader
val computeShader = device.createShaderModule("""
    @compute @workgroup_size(64)
    fn main(@builtin(global_invocation_id) global_id: vec3<u32>) {
        // Compute shader code here
    }
""")

// Create a compute pipeline
val computePipeline = device.createComputePipeline(
    ComputePipelineDescriptor(
        compute = ProgrammableStage(
            module = computeShader,
            entryPoint = "main"
        )
    )
)

// Dispatch compute work
val commandEncoder = device.createCommandEncoder()
val computePass = commandEncoder.beginComputePass()
computePass.setPipeline(computePipeline)
computePass.dispatchWorkgroups(width / 64, height, 1)
computePass.end()

val commandBuffer = commandEncoder.finish()
device.queue.submit(listOf(commandBuffer))
```

## Next Steps

Now that you're familiar with the basics of wgpu4k, you can:

- Explore more advanced rendering techniques
- Learn about textures and samplers
- Implement more complex shaders
- Create interactive applications

Check out the API reference for detailed information about all available classes and methods.

## Resources

- [WebGPU Specification](https://www.w3.org/TR/webgpu/)
- [WebGPU Shading Language (WGSL) Specification](https://www.w3.org/TR/WGSL/)
- [wgpu4k GitHub Repository](https://github.com/wgpu4k/wgpu4k)
