# wgpu4k Architecture Overview

wgpu4k is a Kotlin Multiplatform library that provides a unified interface to WebGPU and native graphics APIs across multiple platforms.

## Architecture Components

The architecture consists of three main layers:

1. **Binding Layer (Kotlin)**
2. **GPU Abstraction Layer**
3. **Platform-Specific Backends**

![Architecture de WGPU4K](wgpu4k-architecture.png)

## Detailed Architecture Breakdown

### 1. Web Platform Support

The web implementation uses WebGPU as its foundation, providing compatibility with modern browsers:

- Firefox
- Chrome/Chromium
- Edge
- Safari

The WebGPU standard ensures consistent behavior across all supported browsers while leveraging each browser's optimized implementation.

### 2. Native Platform Support

wgpu4k provides native implementations for various operating systems:

#### Linux (JVM)
- Vulkan (primary)
- OpenGL (fallback)

#### macOS (JVM + Native)
- Metal (primary)

#### iOS
- Metal (primary)

#### Windows (JVM)
- DirectX 12 (primary)
- Vulkan (alternative)
- OpenGL (fallback)

#### Android
- Vulkan (primary)
- OpenGL ES (fallback)

### 3. Kotlin Multiplatform Integration

The Kotlin layer provides:

- A unified API surface across all platforms
- Type-safe GPU programming
- Coroutine support for asynchronous operations
- Memory management abstractions
- Error handling mechanisms

## External links

* [WGPU Supported Platforms](https://github.com/gfx-rs/wgpu?tab=readme-ov-file#supported-platforms) - Detailed information about all supported operating systems
