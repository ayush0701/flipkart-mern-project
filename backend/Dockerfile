FROM node:16-alpine AS builder

WORKDIR /app


COPY package*.json ./

RUN npm install

COPY . .

RUN npm prune --production

FROM node:16-alpine

WORKDIR /app

# Copy package.json so npm start works
COPY --from=builder /app/package*.json ./

# Copy only production node_modules from builder stage
COPY --from=builder /app/node_modules ./node_modules

# Copy application source code from builder stage
COPY --from=builder /app .


EXPOSE 4000

CMD ["npm","start"]

