# compiler-vis-issues
This is a public repository for compiler-vis project. Since the compiler-vis project is private, we provide this public repository so that users can submit bug reports and feature requests here.

## Usage notes:
* Works best with Google Chrome browser. Firefox sometimes mis-centers the graph.
* For large graphs (~1K nodes), the layout takes some time. The browser may pop up a warning saying the script is unresponsive. Please allow the script to continue. We are working on moving this layout server-side to avoid this issue.

## Requirements/Assumptions on Data Format:

### CFG
* CFG should be given as a .dot file. The instructions should be inside the 'label' field with one instruction per line. 
* This is a sample node `'B108 [shape=box, style=solid, label="main\n400590: mov dword ptr [rbp-0x68], 0xffffff9c 1 0\n400597: mov dword ptr [rbp-0x64], 0x0 1 0"];'`
* The label can start with a newline followed by instructions or it can optionally start with the function name i.e. the function the node belongs to. In the above example, the node belongs to the function main.
* The edge count should be inside the 'label' field of the edge and is optional. 
* This is a sample edge `'B108 -> B113 [style=solid, color="black", label=" ct:1"];'`

### Trace
* Trace should be in ASCII format. It should contain one assembly instruction per line. The second column should contain the instruction address. 
* This is an example line of trace `'0 400460 max _start 31 ed xor ebp, ebp R:RBP=0000000000000000 R:RBP=0000000000000000 W:RBP=0000000000000000 W:GFLAGS=0000000000000246'`
* In the example, second column contains the instruction address 400460. This is used to match the trace with the corresponding node in the CFG.

### BackTainting
* The backtainting feature requires the trace.
* The only thing it relies on is the operand values given last. It looks for the R:, W:, MR, and MR strings to identify these operands. As a result, these need to be in the same format, and need to list all affects that particular function has.

### LoopFinding
* For loopfinding, the current requirement is that the CFG should have exactly one source node (i.e. the node with no incoming edges and one or more outgoing edges).

### Trace Syntax
The full syntax of execution ASCII trace can be found here. 

https://github.com/stephensj2/ScienceUpToPar/wiki/Verbose-ASCII-Trace-Format


