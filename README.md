# Quorum-local-RAFT-network

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

Setup a minimal local [quorum network](https://www.goquorum.com/) with 3 nodes using [raft consensus](https://raft.github.io/) algorithm without tx manager (does not support private transactions).

## Quorum local
Build a local Quorum network based on the [7-nodes example](https://github.com/jpmorganchase/quorum-examples) and simplified to 3 nodes with only [Raft consensus](https://raft.github.io/) without tx manager.

To run these sample network, you must have the following installed:
- [docker](https://docs.docker.com/engine/install/)
- [docker-compose](https://docs.docker.com/compose/install/)
  
## Run the 3 nodes in containers
run:    `docker-compose up -d`

3 Docker Containers
1. quorum_raft_node1_1
   - RPC Port: 22000
   - WS Port: 23000
2. quorum_raft_node2_1
   - RPC Port: 22001
   - WS Port: 23001
3. quorum_raft_node3_1
   - RPC Port: 22002
   - WS Port: 23002


access to geth of nodes: `docker exec -it <container_name> geth attach ./qdata/dd/geth.ipc`

stop:       `docker-compose stop`

remove:     `docker-compose down -v`

sample command in geth console

``` bash
# get node account
> eth.accounts[0]
"0xed9d02e382b34818e88b88a309c7fe71e65f419d"
# get latest block
> eth.getBlock("latest")
# expect output
{
  difficulty: 131072,
  extraData: "0x000...500",
  gasLimit: 3757178881,
  gasUsed: 21000,
  hash: "0xbf2...3d4",
  logsBloom: "0x000...0000",
  miner: "0x000...000",
  mixHash: "0x000...000",
  nonce: "0x0000000000000000",
  number: 1,
  parentHash: "0x6a6...3a2",
  receiptsRoot: "0x056..2d2",
  sha3Uncles: "0x1dc...347",
  size: 726,
  stateRoot: "0x9c0...e58",
  timestamp: 1611559851631510500,
  totalDifficulty: 131072,
  transactions: ["0xeeb...b63"],
  transactionsRoot: "0xc90...215",
  uncles: []
}
# send ethereum
> eth.sendTransaction({from: eth.accounts[0],to: "0x7aa4a14286a25e3a275d7a122c23dc3c107a636a", value: "1000000000000000"})
"0x182bd52c8184ccc9a177c2f0346d5407c6e828649cae8dd5e941029ade81291d"

> eth.getBalance("0x7aa4a14286a25e3a275d7a122c23dc3c107a636a")
1000000000000000

```

