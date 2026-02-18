# IPFS Cluster Topology Orchestrator

Фронтенд для визуального создания и управления топологией IPFS Cluster. Позволяет проектировать сеть узлов, настраивать bootstrap-соединения и деплоить кластер в Kubernetes.

![React](https://img.shields.io/badge/React-18.3-61dafb?logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5.5-3178c6?logo=typescript)
![Vite](https://img.shields.io/badge/Vite-5.3-646cff?logo=vite)
![ReactFlow](https://img.shields.io/badge/ReactFlow-11.11-ff0072)

## Возможности

- **Визуальный редактор топологии** — добавление узлов, соединение рёбрами
- **Семантика рёбер** — ребро A → B означает: узел A бустрапится к B (B — bootstrap)
- **CRUD топологий** — создание, редактирование, удаление
- **Деплой в Kubernetes** — развёртывание и остановка кластера
- **Приватный режим** — опция ClusterIP для доступа только внутри K8s
- **Мониторинг** — статус подов, просмотр логов IPFS и IPFS Cluster

## Требования

- Node.js 18+
- Backend API на порту `3001` (см. [Бэкенд](#бэкенд))

## Установка

```bash
npm install
```

## Запуск

```bash
npm run dev
```

Приложение откроется на [http://localhost:5173](http://localhost:5173).

## Скрипты

| Команда      | Описание                    |
|--------------|-----------------------------|
| `npm run dev`    | Режим разработки (HMR)      |
| `npm run build`  | Сборка для продакшена       |
| `npm run preview`| Превью production-сборки    |

## Структура проекта

```
src/
├── App.tsx          # Главный компонент, список топологий, деплой
├── TopologyCanvas.tsx  # ReactFlow-холст, редактор узлов и рёбер
├── api.ts           # Клиент REST API
├── types.ts         # TypeScript-типы
├── main.tsx         # Точка входа
├── index.css        # Глобальные стили
└── App.css          # Стили приложения
```

## API и бэкенд

Фронтенд проксирует запросы `/v1/*` на бэкенд `http://localhost:3001` (настраивается в `vite.config.ts`).

Основные эндпоинты:
- `GET/POST /v1/topologies` — список и создание топологий
- `GET/PUT/DELETE /v1/topologies/:id` — CRUD топологии
- `POST /v1/topologies/:id/deploy` — деплой в K8s
- `POST /v1/topologies/:id/undeploy` — undeploy
- `GET /v1/topologies/:id/status` — статус подов
- `GET /v1/topologies/:id/pods/:podName/logs` — логи пода

Перед запуском фронтенда убедитесь, что бэкенд запущен на порту 3001.

## Лицензия

MIT
