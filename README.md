## Umbrel Community App Store Template

This repository is a template to create an Umbrel Community App Store. These additional app stores allow developers to distribute applications without submitting to the [Official Umbrel App Store](https://github.com/getumbrel/umbrel-apps).

## How to use:

1. Start by clicking the "Use this template" button located above.
2. Assign an ID and name to your app store within the `umbrel-app-store.yml` file. This file specifies two important attributes:
    - `id` - Acts as a unique prefix for every app within your Community App Store. You must start your application's ID with your app store's ID. For instance, in this template, the app store ID is `sparkles`, and there's an app named `hello world`. Consequently, the app's ID should be: `sparkles-hello-world`.
    - `name` - This is the name of the Community App Store displayed in the umbrelOS UI.
3. Change the name of the `sparkles-hello-world` folder to match your app's ID. The app ID is for you to decide. For example, if your app store ID is `whistles`, and your app is named My Video Downloader, you could set its app ID to `whistles-my-video-downloader`, and rename the folder accordingly.
4. Next, enter your app's listing details in the `whistles-my-video-downloader/umbrel-app.yml`. These are displayed in the umbrelOS UI.
5. Include the necessary Docker services in `whistles-my-video-downloader/docker-compose.yml`.
6. That's it! Your Community App Store, featuring your unique app, is now set up and ready to go. To use your Community App Store, you can add its GitHub url the umbrelOS user interface as shown in the following demo:


https://user-images.githubusercontent.com/10330103/197889452-e5cd7e96-3233-4a09-b475-94b754adc7a3.mp4

## Umbrel 数据目录 / Umbrel data paths

在 `docker-compose.yml` 中请使用变量引用，不要写死绝对路径。
Use the variables in `docker-compose.yml` instead of hard-coding absolute paths.

| 用途 / Purpose | 宿主机路径 / Host path | compose 写法 / In compose |
|---|---|---|
| Umbrel 数据根目录 / Umbrel root | `/home/umbrel/umbrel` | `${UMBREL_ROOT}` |
| 用户共享存储 / Shared storage | `/home/umbrel/umbrel/data/storage` | `${UMBREL_ROOT}/data/storage` |
| 下载目录（下载类应用共用）/ Downloads (shared by downloader apps) | `/home/umbrel/umbrel/data/storage/downloads` | `${UMBREL_ROOT}/data/storage/downloads` |
| 应用私有数据 / Per-app data | `/home/umbrel/umbrel/app-data/<app-id>` | `${APP_DATA_DIR}` |

官方应用（transmission、qBittorrent、Plex、Jellyfin）挂载 `${UMBREL_ROOT}/data/storage/downloads`，Samba 挂载 `${UMBREL_ROOT}/data/storage`。
Official apps (transmission, qBittorrent, Plex, Jellyfin) mount `${UMBREL_ROOT}/data/storage/downloads`; Samba mounts `${UMBREL_ROOT}/data/storage`.

> umbrelOS 1.x 的“文件”应用在界面上使用 `/home/umbrel/umbrel/home`，具体映射关系请在设备上执行 `ls -la ~/umbrel ~/umbrel/home ~/umbrel/data/storage` 确认。
> The umbrelOS 1.x Files app shows `/home/umbrel/umbrel/home`; verify the mapping on your device with `ls -la ~/umbrel ~/umbrel/home ~/umbrel/data/storage`.
