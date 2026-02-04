# gfx803-compatibility-dockerfiles
See: https://hub.docker.com/repositories/chboi
Launch like:

❯ docker run -it \
        --name ITIR \
        -p 7860:7860 \
        --device=/dev/kfd --device=/dev/dri \
        --security-opt seccomp=unconfined \
        --group-add video \
        --env WAYLAND_DISPLAY=$WAYLAND_DISPLAY \
        --env XDG_RUNTIME_DIR=/tmp \
        --env QT_QPA_PLATFORM=wayland \
        -v $XDG_RUNTIME_DIR/$WAYLAND_DISPLAY:/tmp/$WAYLAND_DISPLAY \
        -v /usr/include/vulkan:/usr/include/vulkan:ro \
        -v /usr/include/spirv:/usr/include/spirv:ro \
        -v /usr/include/vk_video:/usr/include/vk_video:ro \
        -v /usr/include/glslang:/usr/include/glslang:ro \
        -v /usr/bin/glslangValidator:/usr/bin/glslangValidator:ro \
        -v "/home/c/Documents/code/ITIR-suite:/home/c/Documents/code/ITIR-suite" \
        -v "/home/c/.codex/:/root/.codex/" \
            --entrypoint /bin/bash \
        dashi_ready_image

        Note please update:

        NODE_VERSION=20.11.1

curl -fsSL https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.xz \
  -o /tmp/node.tar.xz

tar -xJf /tmp/node.tar.xz -C /usr/local --strip-components=1
npm install -g @openai/codex
RG_VERSION=14.1.0
curl -fsSL \
  https://github.com/BurntSushi/ripgrep/releases/download/${RG_VERSION}/ripgrep-${RG_VERSION}-x86_64-unknown-linux-musl.tar.gz \
  -o /tmp/rg.tar.gz
tar -xzf /tmp/rg.tar.gz -C /tmp

cp /tmp/ripgrep-${RG_VERSION}-x86_64-unknown-linux-musl/rg /usr/local/bin/
chmod +x /usr/local/bin/rg
