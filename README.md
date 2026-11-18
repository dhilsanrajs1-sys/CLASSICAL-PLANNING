## ExpNo:10 Implementation of Classical Planning Algorithm

Name: DHILSANRAJ S
Reg no: 212225230058
# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']
```

# Please Prepare Solution or Definition For the method find_plan(initial_state, goal_state, actions)
<h3>You Can use any of the searching Strategies for planning and executing a sequence of actions.<br> You can also look in to the Code given in the Repository.</h3>


# Program :

```

from collections import deque

# Check whether the current state matches the goal state
def is_goal_state(current_state, goal_state):
    return current_state == goal_state


# Check whether an action's preconditions are satisfied
def is_applicable(current_state, precondition):
    return all(
        current_state.get(key) == value
        for key, value in precondition.items()
    )


# Apply an action and generate a new state
def apply_action(current_state, action_effect):
    new_state = current_state.copy()
    new_state.update(action_effect)
    return new_state


# Find a plan using Breadth-First Search
def find_plan(initial_state, goal_state, actions):

    queue = deque([(initial_state.copy(), [])])

    visited_states = {frozenset(initial_state.items())}

    while queue:

        current_state, partial_plan = queue.popleft()

        # Check whether goal is reached
        if is_goal_state(current_state, goal_state):
            return partial_plan

        # Explore all possible actions
        for action_name, action_details in actions.items():

            if is_applicable(
                current_state,
                action_details['precondition']
            ):

                next_state = apply_action(
                    current_state,
                    action_details['effect']
                )

                state_key = frozenset(next_state.items())

                if state_key not in visited_states:

                    visited_states.add(state_key)

                    queue.append((
                        next_state,
                        partial_plan + [action_name]
                    ))

    print("No plan exists.")
    return None


# -----------------------------
# Example 1
# -----------------------------

initial_state = {
    'A': 'Table',
    'B': 'Table'
}

goal_state = {
    'A': 'B',
    'B': 'Table'
}

actions = {
    'move_A_to_B': {
        'precondition': {
            'A': 'Table',
            'B': 'Table'
        },
        'effect': {
            'A': 'B'
        }
    },

    'move_B_to_Table': {
        'precondition': {
            'A': 'Table',
            'B': 'B'
        },
        'effect': {
            'B': 'Table'
        }
    }
}

plan = find_plan(initial_state, goal_state, actions)

print("Example 1:")
print("Plan:", plan)


# -----------------------------
# Example 2
# -----------------------------

initial_state = {
    'A': 'Table',
    'B': 'Table',
    'C': 'Table'
}

goal_state = {
    'A': 'B',
    'B': 'C',
    'C': 'Table'
}

actions = {
    'move_A_to_B': {
        'precondition': {
            'A': 'Table',
            'B': 'Table'
        },
        'effect': {
            'A': 'B'
        }
    },

    'move_B_to_C': {
        'precondition': {
            'A': 'B',
            'B': 'Table',
            'C': 'Table'
        },
        'effect': {
            'B': 'C'
        }
    },

    'move_C_to_Table': {
        'precondition': {
            'A': 'B',
            'B': 'C',
            'C': 'C'
        },
        'effect': {
            'C': 'Table'
        }
    }
}

plan = find_plan(initial_state, goal_state, actions)

print("\nExample 2:")
print("Plan:", plan)
```

# Output :
<img width="1275" height="143" alt="image" src="https://github.com/user-attachments/assets/e71df71d-5726-4448-84fd-bfd4d6ac92b2" />

# Result :
Thus the program has bee executed successfully.


