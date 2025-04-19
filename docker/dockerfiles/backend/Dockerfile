FROM node:18-bullseye-slim AS backend
WORKDIR /app
COPY /app/backend/package*.json ./
RUN npm install
COPY /app/backend/ ./
ENV NODE_OPTIONS=--openssl-legacy-provider

FROM node:18-alpine3.18 
WORKDIR /app
COPY --from=backend /app/node_modules /app/node_modules
COPY --from=backend /app/models/ /app/models
COPY --from=backend /app/routes/ /app/routes
COPY --from=backend /app/db.js /app/db.js
COPY --from=backend /app/index.js /app/index.js
CMD [ "node","index.js" ]

