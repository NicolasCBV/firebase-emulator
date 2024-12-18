# Firebase Emulator Docker Version

This is an unofficial Firebase Emulator Docker image. Use it to emulate all Firebase services in a containerized environment for testing purposes.

## How to Use
You can run the container with minimal configuration using the following commands:

```
docker pull fire-emulator
docker run -p 4000:4000 --env FIREBASE_PROJECT=<YOUR_PROJECT_ID> nicolascbv/fire-emulator
```

### Default Configuration
By default, the emulator uses the following configuration as ```firebase.json```:
```
{
  "firestore": {
    "rules": "firestore.rules",
    "indexes": "firestore.indexes.json"
  },
  "storage": {
    "rules": "storage.rules"
  },
  "database": {
    "rules": "database.rules.json"
  },
  "emulators": {
    "auth": {
      "port": 9099,
      "host": "0.0.0.0"
    },
    "firestore": {
      "port": 8080,
      "host": "0.0.0.0"
    },
    "storage": {
      "port": 9199,
      "host": "0.0.0.0"
    },
    "database": {
      "port": 9000,
      "host": "0.0.0.0"
    }
  }
}
```

### Custom Configuration
#### Volume Strategy
If the default configuration does not meet your requirements, you can provide your own ```firebase.json``` or other configuration files (e.g., ```firestore.rules```, ```storage.rules```) by mapping them to the ```/app``` directory inside the container. For example:

```
docker run -p 4000:4000 -v $(pwd)/my-firebase-config:/home/node/app --env FIREBASE_PROJECT=<YOUR_PROJECT_ID> nicolascbv/fire-emulator
```

Replace <YOUR_PROJECT_ID> with your actual Firebase project ID.

#### Variable Strategy
There is another strategy to set your own custom configuration, you can just provide the FIREBASE_JSON environment variable in json format, it will override the entire default configuration and let you set your custom setup.
