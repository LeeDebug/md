## 每次修改代码后的更新与重启流程

### 首次（或依赖变更后）
```bash
pnpm i
```

### 本地运行调试
```bash
pnpm start
```

### 常规迭代（有代码改动时）
1) 构建前端产物（仓库根目录执行）
```bash
pnpm --filter @md/web build:h5-netlify
```

或（在 apps/web 目录执行）：
```bash
cd apps/web
pnpm run build:h5-netlify
cd ../../
```

2) 使用 docker compose 强制重建并重启（在 docker 目录执行）
```bash
cd docker
docker compose up -d --force-recreate
```

完成后访问：
```
http://localhost:8080
```

备注：当前 compose 通过卷挂载把 `../apps/web/dist` 覆盖到容器的 `/usr/share/nginx/html`，因此每次重新构建后重启即可生效；上传目录 `../public/upload` 已持久化挂载，无需额外操作。


