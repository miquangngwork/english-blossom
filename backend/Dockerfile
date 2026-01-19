# Build and run the Express + Prisma backend, serving the static frontend folder.
# Using the full image improves compatibility for native deps (e.g., bcrypt).
FROM node:20

WORKDIR /app

# Install backend deps first for better caching
COPY backend/package.json backend/package-lock.json ./backend/
COPY backend/prisma ./backend/prisma
RUN cd backend && npm ci

# Copy source
COPY backend ./backend
COPY frontend ./frontend

# Build TS + generate Prisma client
RUN cd backend && npm run build && npx prisma generate

ENV NODE_ENV=production
WORKDIR /app/backend

CMD ["node", "dist/server.js"]
