# === Step 1: Build Frontend ===
FROM node:18 AS frontend
WORKDIR /frontend
COPY frontend/ /frontend
RUN npm install && npm run build

# === Step 2: Build Backend ===
FROM python:3.10 AS backend
WORKDIR /app
COPY backend/ /app
RUN pip install -r requirements.txt

# === Step 3: Combine into Final Image ===
FROM python:3.10
WORKDIR /app

# Copy backend code
COPY --from=backend /app /app

# Copy built frontend to backend's static folder
COPY --from=frontend /frontend/dist /app/static

# Expose port (optional)
EXPOSE 8000

# Run backend
CMD ["python", "app.py"]
