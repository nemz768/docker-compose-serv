#===== BUILD =====
FROM node:20-alpine AS builder

WORKDIR /frontend

COPY package.json package-lock.json tsconfig.json .

RUN npm ci

COPY public/ ./public/ 

COPY src/ ./src/

RUN npm run build


# ===== RUNTIME =====
FROM nginx:alpine

COPY --from=builder /frontend/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]