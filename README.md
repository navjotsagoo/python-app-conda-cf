# Summary
To support deployments of python apps with geo dependencies that are not easily support by python, consider using conda to deploy the app first on unclassified environment and then run the app on the classified network.

When the app is deployed, follow the [instructions here](https://github.com/nsagoo-pivotal/python-app-on-pcf-air-gapped-environments) to export the droplet of your application.

Move the droplet to the classified environment, following the proper agency guidelines and security scanning policies.

## In the classified environment
Create a new folder and extract the contents of the droplet in that directory.
```bash
mkdir -p home/droplet-directory
tar -xvzf /download_path/to/droplet.tgz -C /path/to/home/droplet-directory
```
Extracting the droplet shows four directories in the droplet-directory. These are
```text
app   deps   logs  tmp
```

Add your python application files into the `app` directory.

Repackage the entire contents of the droplet-directory in its original `.tgz` format
```bash
cd home
cd droplet-directory/ && tar -zcvf ../newdroplet.tgz . && cd ..
```

At this point, you should have a new droplet in the `home` directory.

Follow the [instructions here](https://github.com/nsagoo-pivotal/python-app-on-pcf-air-gapped-environments) to deploy this new droplet to cloud foundry in your classified environment.
