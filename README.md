# Nillion-Verified
![image](https://github.com/user-attachments/assets/c8d9dd9b-7d3b-4a11-b1f5-229554a75361)

## Introducing the Nillion Verifier
We’re thrilled to unveil the Nillion Verifier. As a verifier, you will ensure data integrity across the network, playing a crucial role in maintaining security and preparing for mainnet launch.
Early verifiers will have the opportunity to be acknowledged for their contributions, setting themselves apart in the community.
It’s important to note that this is an early prototype phase. During this period, while we’re testing and optimizing the system, we ask you to refrain from uploading PII or other highly sensitive data. Once we roll out the official release, you will be able to securely manage and store sensitive information.

# System Requirements
| Hardware   | Minimum Requirement |
|------------|---------------------|
| CPU        | 4 Cores             |
| RAM        | 6 GB                |
| Disk       | 100 GB              |
| Bandwidth  | 10 MBit/s           |

# Install Guide

## 1.Faucet NIL
Go to the faucet to obtain NIL in your Keplr wallet
https://faucet.testnet.nillion.com/

## 2. Install Docker
```
sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && sudo apt-get update && sudo apt-get install -y docker-ce docker-ce-cli containerd.io && sudo systemctl start docker && sudo systemctl enable docker && sudo docker --version
```
## 3.Verifying Docker install
You should now be able to run the following in a command line to get the version number of your Docker installation:
```
docker --version
```
### Running the hello world container
The next verification step is to be sure that you can run a simple container.
```
docker container run --rm hello-world
```
![image](https://github.com/user-attachments/assets/0b9002b7-8292-4488-abc6-8d868e7842ae)

This will print out “Hello from Docker!” in the terminal output

## 4. Getting the accuser image
To run the accuser you will need to pull the image from the Nillion repo in Docker Hub.
```
docker pull nillion/retailtoken-accuser:v1.0.1
```
## 5.Initialising the accuser
Create a local directory to store state.
``` 
mkdir -p nillion/accuser
```
Then initialise the accuser in the mounted directory.
```
docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.1 initialise
```
This will output the details needed to register the accuser on the website, register them below:
**accound_id: Nillion address of the accuser**
**public_key: Public Key of the accuser**
Note The accuser will store the credentials in a file called credentials.json in the folder that was created. If you lose this file, you will lose access to the keys/address of the accuser.

## 6. Funding the accuser

In order to make accusations on the Nilchain, the accuser account will need to be funded with Nil. You can get this from the Nillion faucet:
https://faucet.testnet.nillion.com/
The Nillion address of the accuser is the one that was generated and entered in the previous step (not your Keplr wallet address).
## 7. Running the accuser

```
docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.1 accuse --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com" --block-start 5527754
```

![image](https://github.com/user-attachments/assets/a6054928-e989-4e72-9a9f-2efea8686b94)

# Check Logs

``` 
docker ps
```
```
docker logs --tail 50 -f <container-id>
```

# GOOD LUCK!




