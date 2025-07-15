## Tree-to-Flow Conversion Implementation

Understanding how AI-generated roadmap data is converted into an interactive flowchart is crucial for creating similar visualization features. Here's the complete implementation guide:

### 8. **Data Structure Overview**

The tree-to-flow conversion uses three main TypeScript interfaces:

```typescript
// Core data structures from app/components/types/roadmap.ts
export type TopicNode = {
  label: string;
  children?: TopicNode[];
};

export type FlowNode = {
  id: string;
  data: { 
    label: string;
    topicNode?: TopicNode;
  };
  position: { x: number; y: number };
  sourcePosition: string;
  targetPosition: string;
};

export type FlowEdge = {
  id: string;
  source: string;
  target: string;
  sourceHandle?: string;
  targetHandle?: string;
};
```

### 9. **Tree-to-Flow Algorithm** (`app/components/utils/tree-to-flow.ts`)

#### **Core Conversion Function**

```typescript
export function generateSpineFlow(topic: string, tree: TopicNode[]) {
  idCounter = 1;
  edgeCounter = 1;
  const nodes: FlowNode[] = [];
  const edges: FlowEdge[] = [];

  const centerX = 800;    // Center X position for spine
  const startY = 50;      // Starting Y position
  const spineSpacing = 20; // Extra spacing between spine nodes
  const dy = 80;          // Vertical spacing between nodes

  // Step 1: Create root node
  const root = createNode(`${topic} Roadmap`, centerX, startY);
  nodes.push(root);

  let currentY = startY + 100;
  let previousNodeId = root.id;

  // Step 2: Process each main topic in the tree
  for (let i = 0; i < tree.length; i++) {
    const topicNode = tree[i];
    const nodeY = currentY;
    
    // Create spine node
    const node = createNode(topicNode.label, centerX, nodeY, topicNode);
    nodes.push(node);

    // Connect to previous spine node vertically
    edges.push({
      id: `spine-${previousNodeId}-${node.id}-${edgeCounter++}`,
      source: previousNodeId,
      target: node.id,
      sourceHandle: "bottom",
      targetHandle: "top",
    });

    previousNodeId = node.id;

    // Step 3: Layout child nodes if they exist
    if (topicNode.children?.length) {
      const direction = i % 2 === 0 ? 1 : -1; // Alternate left/right
      const subtreeHeight = getSubtreeHeight(topicNode, dy);
      const childrenStartY = nodeY - subtreeHeight / 2;

      // Recursively layout children
      layoutSubtreeRecursive(
        node.id,
        centerX,
        childrenStartY,
        topicNode.children,
        direction,
        nodes,
        edges
      );

      currentY += Math.max(subtreeHeight, dy);
    } else {
      currentY += dy;
    }

    currentY += spineSpacing;
  }

  return { nodes, edges };
}
```

#### **Helper Functions**

```typescript
// Creates a new FlowNode with unique ID and positioning
function createNode(
  label: string,
  x: number,
  y: number,
  topicNode?: TopicNode
): FlowNode {
  return {
    id: `${idCounter++}`,
    data: { label, topicNode },
    position: { x, y },
    sourcePosition: 'bottom',
    targetPosition: 'top',
  };
}

// Calculates total height needed for a subtree
function getSubtreeHeight(topic: TopicNode, nodeHeight = 80): number {
  if (!topic.children || topic.children.length === 0) return nodeHeight;
  return topic.children.reduce(
    (sum, child) => sum + getSubtreeHeight(child, nodeHeight),
    0
  );
}

// Recursively layouts child nodes in horizontal branches
function layoutSubtreeRecursive(
  parentId: string,
  parentX: number,
  startY: number,
  children: TopicNode[],
  direction: 1 | -1,  // 1 = right, -1 = left
  nodes: FlowNode[],
  edges: FlowEdge[],
  depth = 1
): number {
  const dx = 300; // Horizontal spacing between levels
  const dy = 100; // Vertical spacing between siblings

  let currentY = startY;

  for (const child of children) {
    const subtreeHeight = getSubtreeHeight(child, dy);
    const nodeX = parentX + direction * dx * depth;
    const nodeY = currentY + subtreeHeight / 2;

    const node = createNode(child.label, nodeX, nodeY, child);
    nodes.push(node);

    // Create edge with proper handle connections
    edges.push({
      id: `child-${parentId}-${node.id}-${edgeCounter++}`,
      source: parentId,
      target: node.id,
      sourceHandle: direction === 1 ? "right" : "left-source",
      targetHandle: direction === 1 ? "left" : "right-target",
    });

    // Recursively layout grandchildren
    if (child.children?.length) {
      layoutSubtreeRecursive(
        node.id,
        nodeX,
        currentY,
        child.children,
        direction,
        nodes,
        edges,
        depth + 1
      );
    }

    currentY += subtreeHeight;
  }

  return currentY;
}
```

### 10. **Layout Strategy Explained**

#### **Spine-Based Layout**
The algorithm creates a **central vertical spine** with main topics, then branches child topics horizontally:

```
    Root Topic
        |
   Main Topic 1 ——— Child 1.1 ——— Grandchild 1.1.1
        |            └——— Child 1.2
        |
   Main Topic 2 
        |            ┌——— Child 2.1
        |    ┌——————— Child 2.2 ——— Grandchild 2.2.1
   Main Topic 3      └——— Child 2.3
        |
   Main Topic 4 ——— Child 4.1
```

#### **Key Features:**
1. **Alternating Sides**: Child topics alternate between left and right sides of the spine
2. **Dynamic Spacing**: Vertical spacing adjusts based on subtree height
3. **Recursive Layout**: Supports unlimited nesting levels
4. **Handle Management**: Proper connection points for smooth edge routing

### 11. **Usage Example**

```typescript
// Example AI response structure
const aiGeneratedTree: TopicNode[] = [
  {
    label: "HTML Fundamentals",
    children: [
      { label: "Elements & Attributes" },
      { label: "Semantic HTML" },
      { label: "Forms & Validation" }
    ]
  },
  {
    label: "CSS Styling",
    children: [
      { 
        label: "Layout Systems",
        children: [
          { label: "Flexbox" },
          { label: "Grid" },
          { label: "Positioning" }
        ]
      },
      { label: "Responsive Design" }
    ]
  },
  {
    label: "JavaScript Basics",
    children: [
      { label: "Variables & Functions" },
      { label: "DOM Manipulation" },
      { label: "Event Handling" }
    ]
  }
];

// Convert to flowchart
const { nodes, edges } = generateSpineFlow("Frontend Development", aiGeneratedTree);

// Use with React Flow
<ReactFlow 
  nodes={nodes} 
  edges={edges} 
  nodeTypes={{ custom: CustomNode }}
/>
```

### 12. **Customization Options**

You can modify the layout by adjusting these constants:

```typescript
const layoutConfig = {
  centerX: 800,        // Horizontal center position
  startY: 50,          // Top margin
  spineSpacing: 20,    // Extra space between spine nodes  
  horizontalGap: 300,  // Distance between levels
  verticalGap: 100,    // Distance between siblings
  nodeHeight: 80       // Standard node height
};
```

### 13. **Integration with React Flow**

The generated nodes and edges integrate seamlessly with React Flow:

```typescript
import ReactFlow, { Background, Controls, MiniMap } from 'reactflow';
import 'reactflow/dist/style.css';

function RoadmapVisualization({ aiResponse }) {
  const { nodes, edges } = generateSpineFlow(
    aiResponse.topic, 
    aiResponse.structure
  );

  return (
    <div style={{ height: '100vh' }}>
      <ReactFlow
        nodes={nodes}
        edges={edges}
        nodeTypes={{ custom: CustomNode }}
        fitView
        attributionPosition="bottom-left"
      >
        <Background />
        <Controls />
        <MiniMap />
      </ReactFlow>
    </div>
  );
}
```

This implementation provides a flexible, scalable foundation for converting hierarchical learning data into interactive visualizations that users can explore and navigate intuitively.
