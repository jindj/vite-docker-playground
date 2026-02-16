# Docker pense-bête (Dev / Tests / Prod)

## Quick commands

- Lancer (build + up) : `docker compose up --build`
- Logs : `docker compose logs -f`
- Stop : `docker compose down`
- Reset complet (supprime aussi node_modules en volume) : `docker compose down -v && docker compose up --build`

## Container (debug)

- Voir containers actifs : `docker ps`
- Voir aussi ceux arrêtés : `docker ps -a`
- Logs d’un container : `docker logs <container>`
- Shell dans un container : `docker exec -it <container> sh`

## Tests (Vitest)

- Lancer le service tests : `docker compose up --build test-app`
- Si `vitest: not found` : reset volume `node_modules` → `docker compose down -v && docker compose up --build test-app`
- Si tu ne vois pas `test-app` : normal (container “one-shot”) → `docker ps -a` + `docker logs test-app`

## Dev

- Build image dev : `docker build -t myreact .`
- Run dev (HMR + volumes) : `docker run --rm --name react-app -p 5173:5173 --mount type=bind,src="$(pwd)",target=/app --mount type=volume,target=/app/node_modules myreact`
- Dev via compose : `docker compose up --build`
- Logs dev : `docker compose logs -f`
- Stop dev : `docker compose down`
- Reset dev (⚠️ supprime aussi le volume node_modules) : `docker compose down -v && docker compose up --build`

## Prod

- Build image prod : `docker build -t nginxreact -f Dockerfile.prod .`
- Run prod : `docker run --rm -p 8080:80 nginxreact`
- Prod via compose : `docker compose -f docker-compose.prod.yml up --build -d`
- Logs prod : `docker compose -f docker-compose.prod.yml logs -f`
- Stop prod : `docker compose -f docker-compose.prod.yml down`

## Nettoyage

- Containers inutilisés : `docker container prune`
- Volumes inutilisés : `docker volume prune`
- Nettoyage complet (⚠️ agressif) : `docker system prune -a`

## Rappels (pièges fréquents)

- `docker ps` n’affiche que les containers en cours d’exécution (utilise `docker ps -a` pour voir les “Exited”).
- Erreurs de permissions / EACCES en dev : souvent lié au volume `node_modules` → `docker compose down -v` puis relancer.
