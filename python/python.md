# How to create Python package

# Integrate Flask with gunicorn
Taken from https://flask.palletsprojects.com/en/2.3.x/deploying/gunicorn/#running

1. run venv
2. install your python application and gunicorn
3. create `gunicorn_config.py` and enter following data into it:
bind = "0.0.0.0:5001"
workers = 4
threads = 4
timeout = 120
4. add `gunicorn` to requirements.txt
5. run app with following code: `gunicorn track_workout:app`
- taken from <app_name>/views.py

# Push Dockerized Flask+gunicorn web app to Azure
1. build Docker container: `docker build --tag azure/track_workout .`
2. create docker instance in registry called "sportas": `az acr create --resource-group pbernecki_rg_5400 --name sportas --sku Basic`
3. grant "sportas" as admin, in its 
- can be done in CLI.. ?
4. build container compatible with linux/amd64 and push it to Azure `docker buildx build --push --platform linux/amd64 -t sportas.azurecr.io/azure/track_workout:latest .`
5. Go to Azure > App services > Create: Web app. In this case, app will be called "sportuok"