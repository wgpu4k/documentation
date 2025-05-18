# Getting Started with wgpu4k

Welcome to the wgpu4k documentation! wgpu4k is a Kotlin binding for WebGPU, providing a type-safe and idiomatic Kotlin API for GPU programming.

## What is wgpu4k?

wgpu4k is a Kotlin library that provides bindings to the WebGPU API, allowing you to write GPU-accelerated applications in Kotlin. It's designed to be:

- **Type-safe**: Leverages Kotlin's strong type system to catch errors at compile time
- **Idiomatic**: Follows Kotlin conventions and patterns
- **Efficient**: Provides high-performance access to GPU capabilities
- **Cross-platform**: Works on multiple platforms where WebGPU is supported

## Why using wgpu4k?

wgpu4k serves as an excellent foundation for building high-level frameworks that leverage GPU capabilities. It can be
used to create:

- Graphics frameworks for 2D and 3D rendering
- Machine learning and AI computation libraries
- Image processing tools
- Scientific computing applications
- Any specialized framework that can benefit from GPU's parallel processing architecture

The low-level access to GPU capabilities combined with Kotlin's type safety and modern language features makes wgpu4k an
ideal base for developing higher-level abstractions and domain-specific solutions.

Additionally, wgpu4k's straightforward and intuitive API design makes it accessible for developers to create standalone
applications without needing extensive GPU programming experience. The simple, yet powerful interface allows you to
quickly build and deploy GPU-accelerated applications while maintaining full control over the underlying hardware
capabilities.

## Quick Start Guide

For those who want to get started immediately, check out our [Quickstart Guide](quickstart.md).

## Core Libraries

- [wgpu4k](https://github.com/wgpu4k/wgpu4k) - High-level WebGPU binding compatible with all platforms, including browsers.
- [wgpu4k-toolkit](https://github.com/wgpu4k/wgpu4k-toolkit) - Utilities for easily creating windows and WebGPU context. Avoid if you prefer to manage these aspects yourself.

## Foundation Libraries

- [webgpu-ktypes](https://github.com/wgpu4k/webgpu-ktypes) - Interfaces generated from WebGPU specifications. Serves as the foundation for wgpu4k implementation, but can be reused to create custom bindings (e.g., with a backend like Dawn).
- [webgpu-ktypes-web](https://github.com/wgpu4k/webgpu-ktypes-web) - Web binding generated from WebGPU specifications, supporting kotlin/JS and kotlin/WasmJS through a common API.
- [wgpu4k-native](https://github.com/wgpu4k/wgpu4k-native) - Low-level native binding for Linux/macOS/Windows/Android/iOS.

## Resources

- [Examples using wgpu4k](https://github.com/wgpu4k/wgpu4k-samples.git)
- [WebGPU Specification](https://www.w3.org/TR/webgpu/)
- [WebGPU Shading Language (WGSL) Specification](https://www.w3.org/TR/WGSL/)
- [wgpu4k GitHub Repository](https://github.com/wgpu4k/wgpu4k)