# Safe GitHub Actions Template

This template repository can be forked to easily setup monitoring for a Safe via GitHub actions.

The template includes the use of the following GitHub actions:

- [Safe Transaction Simulator](https://github.com/rmeissner/safe-simulator-gh-action/blob/main/action.yml)
  - This GitHub action will Simulate Multisig, Module and SafeSnap transactions
- [Safe Service Monitor](https://github.com/rmeissner/safe-service-monitor-gh-action/blob/main/action.yml)
  - This GitHub will monitor the Safe service for new pending transactions
- [Snapshot Monitor](https://github.com/rmeissner/safe-snapshot-monitor-gh-action/blob/main/action.yml)
  - This GitHub will monitor Snapshot for new proposals


### Set up

1. Fork the repository and rename to your liking

2. The following secrets should be set on your GitHub repository:

- `PERSONAL_ACCESS_TOKEN` - [GitHub access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token), used to trigger sub flows
- `TARGET_SAFE` - Checksummed address of the Safe to monitor
- `SNAPSHOT_SPACE` - Name of the Snapshot space that should be monitored
- `JSON_RPC_NODE` - Ethereum JSON RPC endpoint (e.g. [Infura](https://infura.io/dashboard))
- `SERVICE_URL` - URL of the Safe service to monitor

3. Enabled the workflows in the `Actions` tab 

4. Manually trigger the first sync with the Safe services using the `Safe Service Sync` workflow

![image](https://user-images.githubusercontent.com/2896048/145611966-729aa59e-a9f7-4ad0-a18e-85aa5ab9e7fd.png)



### Workflows

Workflows can be disabled or removed if not required.

#### [Safe Service Sync](./.github/workflows/monitor.yml)

This workflow configures the [Safe Service Monitor](https://github.com/rmeissner/safe-service-monitor-gh-action/blob/main/action.yml) action. It is setup to check every 5 minutes if a new pending multisig transaction is available and create a new PR with the details of that multisig transaction.

#### [Snapshot Sync](./.github/workflows/snapshot.yml)

This workflow configures the [Snapshot Monitor](https://github.com/rmeissner/safe-snapshot-monitor-gh-action/blob/main/action.yml) action. It is setup to check every 5 minutes if a new proposal is available at the specified Snapshot space and create a new PR with the details of that proposal

#### [Safe Tx Simulation](./.github/workflows/simulator.yml)

This workflow configures the [Safe Transaction Simulator](https://github.com/rmeissner/safe-simulator-gh-action/blob/main/action.yml) action. It is setup to check run a simulation for each `push` to a branch that is not to `main` (assumed to be the deault branch).
