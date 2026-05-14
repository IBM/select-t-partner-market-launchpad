# Troubleshooting & FAQ

This page covers the most common issues encountered across all labs. If your issue isn't listed here, ask your facilitator.

## 1. watsonx Orchestrate ADK commands are failing

Check if the ADK is able to connect to your wxO server. In terminal run,
```
orchestrate agents list
```

If you see agents listed then your ADK is connected to your wxO server. If you get error such as:
```
ClientAPIException(status_code=401, message={"code":401,"message":"wxO unauthorized - PEM value not found for the given kid"})
```

1. Check if the API Key has expired.
2. Try activating env again with this command:
    ```
    orchestrate env activate bootcamp --apikey <your-api-key>
    ```

If none of the above work try creating a new env with a new name.
```
orchestrate env add --name <new-name> --url https://api.{REGION}.watson-orchestrate.ibm.com/instances/{INSTANCE_ID} -t ibm_iam
orchestrate env activate <new-name> --apikey <your-api-key>
```

## 2. Lab commands are not working

Ensure you are in the right directory before executing the lab commands. For example if you are executing the vehicle maintenance agent lab, ensure you're in the `vehicle_maintenance_agent/` directory and it will have `agents`, `tools`, `knowledge-base` directories.
