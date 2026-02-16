# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) (or [oxc](https://oxc.rs) when used in [rolldown-vite](https://vite.dev/guide/rolldown)) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## React Compiler

The React Compiler is currently not compatible with SWC. See [this issue](https://github.com/vitejs/vite-plugin-react/issues/428) for tracking the progress.

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.

---

                                                                    DOCKER FROM SCRATCH

---

# Construction du Docker puis lancer un container depuis l'image

docker build -t myreact . && docker run -it -p 5173:5173 --name react-app myreact

docker build -t nginxreact -f Dockerfile.prod . # PROD
docker run --rm -p 8080:80 nginxreact # RUN PROD

# Live reload

docker run --rm --name react-app-3 -p 5173:5173 --mount type=bind,src="$(pwd)",target=/app --mount type=volume,target=/app/node_modules myreact

# Connection au container via sh

docker exec -it react-app-3 sh

# Commands

docker compose -f docker-compose.prod.yml up --build -d
docker compose -f docker-compose.prod.yml logs -f
docker compose -f docker-compose.prod.yml down

docker container/volume prune
docker system prune -a
docker compose down -v

---

                                                                    DOCKER COMPOSE

---

docker compose up -d / build

---

                                                                    TESTS LIBS

---

npm install --save-dev vitest @testing-library/react @testing-library/jest-dom jsdom
