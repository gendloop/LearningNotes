# Summary

## GitHub

1. 下载公开仓库发布版本中的资源

    `curl -KLJO https://github.com/USER/REPO/archive/refs/tags/ASSET`

2. 下载私有仓库发布版本中的资源

    ```bash
    # 获取资源ID
    curl -kH "Authorization: token TOKEN" \
        -L https://api.github.com/repos/USER/REPO/releases/tags/TAG \
    # 下载资源
    curl -kH "Authorization: token TOKEN" \
        -H "Accept: application/octet-stream" \
        -L https://api.github.com/repos/USER/REPO/releases/assets/ASSET_ID \
        -o ASSET_NAME
    ```

3. 下载公开仓库中的文件

    ```bash
    curl -kJO \
        -H "Authorization: token TOKEN" \
        -L https://raw.githubusercontent.com/USER/REPO/BRANCH/PATH_TO_FILE
    ```

4. 列出仓库中的密钥

    ```bash
    curl -KL \
        -H "Accept: application/vnd.github+json" \
        -H "Authorization: Bearer TOKEN" \
        -H "X-GitHub-Api-Version: 2022-11-28" \
        https://api.github.com/repos/USER/REPO/actions/secrets
    ```
