# 📝 Example Task Decompositions

**Model:** OpenClaw-Planner-v1
**Purpose:** Demonstrate task decomposition capabilities for Konnex AI Miner submission

---

## Example 1: Simple Pick-and-Place

### **Input:**
```
"Pick up the red cube from the table and place it in the blue bin"
```

### **Output:**
```json
{
  "task_id": "pick-place-001",
  "difficulty": "easy",
  "subtasks": [
    {
      "id": 1,
      "name": "Navigate to table",
      "prerequisites": [],
      "required_skills": ["navigation"],
      "estimated_time": "5s"
    },
    {
      "id": 2,
      "name": "Identify red cube",
      "prerequisites": [1],
      "required_skills": ["vision"],
      "estimated_time": "2s"
    },
    {
      "id": 3,
      "name": "Grasp red cube",
      "prerequisites": [2],
      "required_skills": ["grasp"],
      "estimated_time": "3s"
    },
    {
      "id": 4,
      "name": "Navigate to blue bin",
      "prerequisites": [3],
      "required_skills": ["navigation"],
      "estimated_time": "5s"
    },
    {
      "id": 5,
      "name": "Release cube in bin",
      "prerequisites": [4],
      "required_skills": ["grasp"],
      "estimated_time": "2s"
    }
  ],
  "validation": {
    "feasible": true,
    "estimated_total_time": "17s",
    "required_robots": 1,
    "risk_factors": []
  }
}
```

---

## Example 2: Kitchen Cleanup

### **Input:**
```
"Clean the kitchen counter: throw away trash, put dishes in sink, and wipe the surface"
```

### **Output:**
```json
{
  "task_id": "kitchen-cleanup-001",
  "difficulty": "medium",
  "subtasks": [
    {
      "id": 1,
      "name": "Identify trash items on counter",
      "prerequisites": [],
      "required_skills": ["vision", "classification"],
      "estimated_time": "5s"
    },
    {
      "id": 2,
      "name": "Pick up trash",
      "prerequisites": [1],
      "required_skills": ["grasp"],
      "estimated_time": "10s"
    },
    {
      "id": 3,
      "name": "Dispose trash in bin",
      "prerequisites": [2],
      "required_skills": ["navigation"],
      "estimated_time": "10s"
    },
    {
      "id": 4,
      "name": "Identify dishes on counter",
      "prerequisites": [],
      "required_skills": ["vision", "classification"],
      "estimated_time": "5s"
    },
    {
      "id": 5,
      "name": "Pick up dishes",
      "prerequisites": [4],
      "required_skills": ["grasp"],
      "estimated_time": "15s"
    },
    {
      "id": 6,
      "name": "Place dishes in sink",
      "prerequisites": [5],
      "required_skills": ["navigation"],
      "estimated_time": "10s"
    },
    {
      "id": 7,
      "name": "Fetch cleaning cloth",
      "prerequisites": [],
      "required_skills": ["navigation", "grasp"],
      "estimated_time": "10s"
    },
    {
      "id": 8,
      "name": "Wipe counter surface",
      "prerequisites": [3, 6, 7],
      "required_skills": ["manipulation"],
      "estimated_time": "30s"
    }
  ],
  "validation": {
    "feasible": true,
    "estimated_total_time": "95s",
    "required_robots": 1,
    "risk_factors": ["fragile_dishes", "wet_surface"]
  }
}
```

---

## Example 3: Multi-Robot Warehouse Task

### **Input:**
```
"Move 10 boxes from shelf A to shelf B, then scan inventory"
```

### **Output:**
```json
{
  "task_id": "warehouse-001",
  "difficulty": "hard",
  "subtasks": [
    {
      "id": 1,
      "name": "Robot 1: Navigate to shelf A",
      "prerequisites": [],
      "required_skills": ["navigation"],
      "estimated_time": "10s",
      "assigned_robot": "mobile-001"
    },
    {
      "id": 2,
      "name": "Robot 1: Pick up box 1",
      "prerequisites": [1],
      "required_skills": ["grasp"],
      "estimated_time": "5s",
      "assigned_robot": "mobile-001"
    },
    {
      "id": 3,
      "name": "Robot 1: Navigate to shelf B",
      "prerequisites": [2],
      "required_skills": ["navigation"],
      "estimated_time": "10s",
      "assigned_robot": "mobile-001"
    },
    {
      "id": 4,
      "name": "Robot 1: Place box on shelf B",
      "prerequisites": [3],
      "required_skills": ["manipulation"],
      "estimated_time": "5s",
      "assigned_robot": "mobile-001"
    },
    {
      "id": 5,
      "name": "Repeat steps 2-4 for boxes 2-10",
      "prerequisites": [4],
      "required_skills": ["navigation", "grasp", "manipulation"],
      "estimated_time": "270s",
      "assigned_robot": "mobile-001"
    },
    {
      "id": 6,
      "name": "Robot 2: Navigate to shelf B",
      "prerequisites": [5],
      "required_skills": ["navigation"],
      "estimated_time": "10s",
      "assigned_robot": "scanner-001"
    },
    {
      "id": 7,
      "name": "Robot 2: Scan all boxes on shelf B",
      "prerequisites": [6],
      "required_skills": ["vision", "scanning"],
      "estimated_time": "60s",
      "assigned_robot": "scanner-001"
    }
  ],
  "validation": {
    "feasible": true,
    "estimated_total_time": "380s",
    "required_robots": 2,
    "risk_factors": ["heavy_boxes", "coordination_required"],
    "coordination_notes": "Robot 2 must wait for Robot 1 to complete box moving"
  }
}
```

---

## Example 4: Error Recovery Scenario

### **Input:**
```
"Pour water from pitcher into glass"
```

### **Output (with error recovery):**
```json
{
  "task_id": "pour-water-001",
  "difficulty": "medium",
  "subtasks": [
    {
      "id": 1,
      "name": "Navigate to pitcher location",
      "prerequisites": [],
      "required_skills": ["navigation"],
      "estimated_time": "5s"
    },
    {
      "id": 2,
      "name": "Grasp pitcher handle",
      "prerequisites": [1],
      "required_skills": ["grasp"],
      "estimated_time": "3s"
    },
    {
      "id": 3,
      "name": "Lift pitcher",
      "prerequisites": [2],
      "required_skills": ["manipulation"],
      "estimated_time": "2s"
    },
    {
      "id": 4,
      "name": "Navigate to glass location",
      "prerequisites": [3],
      "required_skills": ["navigation"],
      "estimated_time": "5s"
    },
    {
      "id": 5,
      "name": "Position pitcher above glass",
      "prerequisites": [4],
      "required_skills": ["precise_manipulation"],
      "estimated_time": "5s"
    },
    {
      "id": 6,
      "name": "Tilt pitcher to pour",
      "prerequisites": [5],
      "required_skills": ["precise_manipulation"],
      "estimated_time": "10s"
    },
    {
      "id": 7,
      "name": "Return pitcher to original position",
      "prerequisites": [6],
      "required_skills": ["manipulation"],
      "estimated_time": "5s"
    }
  ],
  "validation": {
    "feasible": true,
    "estimated_total_time": "35s",
    "required_robots": 1,
    "risk_factors": ["liquid_spill", "fragile_glass", "weight_shift"]
  },
  "error_recovery": {
    "if_grasp_fails": "Try alternative grasp point on pitcher handle",
    "if_spill_detected": "Abort task, fetch cleaning cloth, retry with slower tilt",
    "if_glass_moves": "Re-localize glass position, adjust pouring trajectory"
  }
}
```

---

## Example 5: Bedroom Organization

### **Input:**
```
"Organize the bedroom: make the bed, hang clothes in closet, and put shoes on rack"
```

### **Output:**
```json
{
  "task_id": "bedroom-org-001",
  "difficulty": "hard",
  "subtasks": [
    {
      "id": 1,
      "name": "Strip old bedding (if needed)",
      "prerequisites": [],
      "required_skills": ["grasp", "manipulation"],
      "estimated_time": "60s"
    },
    {
      "id": 2,
      "name": "Straighten bed sheet",
      "prerequisites": [1],
      "required_skills": ["manipulation"],
      "estimated_time": "30s"
    },
    {
      "id": 3,
      "name": "Place pillows on bed",
      "prerequisites": [2],
      "required_skills": ["grasp", "manipulation"],
      "estimated_time": "20s"
    },
    {
      "id": 4,
      "name": "Arrange blanket neatly",
      "prerequisites": [3],
      "required_skills": ["manipulation"],
      "estimated_time": "30s"
    },
    {
      "id": 5,
      "name": "Collect clothes from floor/furniture",
      "prerequisites": [],
      "required_skills": ["vision", "grasp"],
      "estimated_time": "60s"
    },
    {
      "id": 6,
      "name": "Navigate to closet",
      "prerequisites": [5],
      "required_skills": ["navigation"],
      "estimated_time": "10s"
    },
    {
      "id": 7,
      "name": "Hang clothes in closet",
      "prerequisites": [6],
      "required_skills": ["manipulation"],
      "estimated_time": "60s"
    },
    {
      "id": 8,
      "name": "Collect shoes",
      "prerequisites": [],
      "required_skills": ["vision", "grasp"],
      "estimated_time": "30s"
    },
    {
      "id": 9,
      "name": "Place shoes on shoe rack",
      "prerequisites": [8],
      "required_skills": ["navigation", "manipulation"],
      "estimated_time": "20s"
    }
  ],
  "validation": {
    "feasible": true,
    "estimated_total_time": "320s",
    "required_robots": 1,
    "risk_factors": ["cloth_deformation", "multiple_object_types"]
  }
}
```

---

## Summary Statistics

| Example | Difficulty | Subtasks | Time Est. | Robots | Risk Factors |
|---------|------------|----------|-----------|--------|--------------|
| Pick-and-Place | Easy | 5 | 17s | 1 | None |
| Kitchen Cleanup | Medium | 8 | 95s | 1 | 2 |
| Warehouse | Hard | 7 | 380s | 2 | 2 |
| Pour Water | Medium | 7 | 35s | 1 | 3 |
| Bedroom Org | Hard | 9 | 320s | 1 | 2 |

**Total Examples:** 5
**Coverage:** Simple tasks, multi-step tasks, multi-robot tasks, error recovery, household tasks

---

*Created: 2026-03-23 | For Konnex AI Miner Submission*

