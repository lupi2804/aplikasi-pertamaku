# Tahap build untuk aplikasi Vite
FROM node:18-alpine AS build

# Set direktori kerja
WORKDIR /app

# Salin file package.json dan package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Salin semua file aplikasi
COPY . .

# Build aplikasi Vite
RUN npm run build

# Pastikan direktori output ada
RUN if [ ! -d "/app/dist" ]; then echo "Build folder dist tidak ditemukan"; exit 1; fi

# Tahap untuk menjalankan aplikasi menggunakan server produksi
FROM node:18-alpine

# Direktori kerja
WORKDIR /app

# Salin hasil build dari tahap build sebelumnya
COPY --from=build /app/dist ./dist

# Install http-server untuk melayani file statis
RUN npm install -g http-server

# Expose port 80 (Vite dapat berjalan di port ini)
EXPOSE 80

# Perintah untuk menjalankan aplikasi Vite
CMD ["http-server", "dist", "-p", "80"]

