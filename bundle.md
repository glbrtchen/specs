# Filesystem Bundle（文件系统包？）

## Container Format（容器格式）

This section defines a format for encoding a container as a *filesystem bundle* - a set of files organized in a certain way, and containing all the necessary data and metadata for any compliant runtime to perform all standard operations against it.
See also [OS X application bundles](http://en.wikipedia.org/wiki/Bundle_%28OS_X%29) for a similar use of the term *bundle*.

The definition of a bundle is only concerned with how a container, and its configuration data, are stored on a local file system so that it can be consumed by a compliant runtime.（文件系统包的定义只包含容器和配置数据如何存放到本地文件系统，便于合适的运行时执行）

A Standard Container bundle contains all the information needed to load and run a container.
This includes the following three artifacts which MUST all reside in the same directory on the local filesystem:

1. `config.json` : contains host independent configuration data.
This REQUIRED file, which MUST be named `config.json`, contains settings that are host independent and application specific such as security permissions, environment variables and arguments.
When the bundle is packaged up for distribution, this file MUST be included.
See [`config.json`](config.md) for more details.
（独立于主机的配置信息，见config.json文件）

2. `runtime.json` : contains host-specific configuration data.
This REQUIRED file, which MUST be named `runtime.json`, contains settings that are host specific such as mount sources and hooks.
The goal is that the bundle can be moved as a unit to another runtime and run the same application once a host-specific `runtime.json` is defined.
When the bundle is packaged up for distribution, this file MUST NOT be included.
See [`runtime.json`](runtime-config.md) for more details.
（依赖于主机的配置信息，见runtime.json文件）

3. A directory representing the root filesystem of the container.
While the name of this REQUIRED directory may be arbitrary, users should consider using a conventional name, such as `rootfs`.
When the bundle is packaged up for distribution, this directory MUST be included.
This directory MUST be referenced from within the `config.json` file.

While these three artifacts MUST all be present in a single directory on the local filesytem, that directory itself is not part of the bundle.
In other words, a tar archive of a *bundle* will have these artifacts at the root of the archive, not nested within a top-level directory.

文件系统包三要素：config.json(针对容器的配置)、runtime.json(针对主机的配置)、存放root文件系统的目录
