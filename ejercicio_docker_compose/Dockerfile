FROM python:3.11

# Establecer directorio de trabajo
WORKDIR /app

# Copiar archivos
COPY myapp.py /app/
COPY requirements.txt /app/

# Instalar dependencias
RUN pip install --no-cache-dir -r requirements.txt

# Exponer el puerto 5000 para la aplicación
EXPOSE 5000

# Comando para ejecutar la aplicación Flask
CMD ["python", "myapp.py"]
