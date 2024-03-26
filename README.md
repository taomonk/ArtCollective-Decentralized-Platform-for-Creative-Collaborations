# ArtCollective-Decentralized-Platform-for-Creative-Collaborations
ArtCollective is a Web3-based platform that connects artists, musicians, and writers, enabling them to collaborate on projects and fairly share ownership and royalties using smart contracts.
from brownie import ArtCollaboration, accounts

def deploy_art_collaboration():
    account = accounts[0]  # Assuming the first account is used for deployment
    art_collaboration = ArtCollaboration.deploy({'from': account})
    print(f"Deployed at {art_collaboration.address}")
    return art_collaboration

def add_participants(contract, participants):
    account = accounts[0]
    for participant, share in participants.items():
        contract.addParticipant(participant, share, {'from': account})
        print(f"Added participant {participant} with share {share}")

def finalize_project(contract):
    account = accounts[0]
    contract.finalizeProject({'from': account})
    print("Project finalized.")

def distribute_royalties(contract, amount):
    account = accounts[0]
    contract.distributeRoyalties({'from': account, 'value': amount})
    print("Royalties distributed.")

def main():
    participants = {
        '0xAddress1': 50,  # Example participant Ethereum addresses and their share percentages
        '0xAddress2': 50,
    }
    contract = deploy_art_collaboration()
    add_participants(contract, participants)
    finalize_project(contract)
    distribute_royalties(contract, 1e18)  # Example amount in wei

if __name__ == "__main__":
    main()
