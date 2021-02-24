# Homie

'Homie' is a bot running on Discord with a MongoDB backend.

Installation instructions:

# Declaring a new Discord bot

* Sign into https://discord.com/developers/applications 
* Click on 'New Aplication' and name you bot
* In 'Bot' click on 'Add bot'
* Uncheck 'Public bot'
* Click on 'Click to reveal token' and copy the generated token key
* In the Python application's 'app' folder, create an '.env' and '.env_debug' text files, and in bot enter: DISCORD_TOKEN_PERSONNAL= immediately followed by your token key.


# Importing the dataset into MongoDB

Prerequisite: it is assumed a MongoDB instance is installed and running locally in Docker.

* Download the files from the Github project's dataset folder to your local environment and unzip them.
* Ensure MongoDB is running
* Copy each extracted JSON file to MongoDB's tmp directory:

sudo docker cp <JSON filename> mongodb:/tmp/<JSON filename>

* Import each file into MongoDB in its own collection, but in a shared DB:

sudo docker exec mongodb mongoimport -d homie -c <collection-name> --file /tmp/<JSON filename> --jsonArray

* Example:

sudo docker cp data_science.json mongodb:/tmp/data_science.json
sudo docker exec mongodb mongoimport -d homie -c data_science --file /tmp/data_science.json --jsonArray

* From the MongoDB CLI, create an index for each created collection:

db.<collection>.createIndex({Title:"text"})

