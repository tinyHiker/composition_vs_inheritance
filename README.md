![The Weakness of Inheritance](./Composition_vs_inheritance.png)


# Composition vs. Inheritance in an Employee Management System

In this repository, we explore two central design paradigms of object-oriented programming - Composition and Inheritance. By diving into the realm of an Employee Management System, we get to see the merits and demerits of each approach.

## Overview

The code exemplifies a ubiquitous challenge in object-oriented programming - managing class responsibilities and attributes via inheritance. While inheritance can sometimes be intuitive, it can lead to redundant subclasses and convoluted logic if not implemented with care.

Take the base `Employee` class for instance. In the inheritance model, it is subclassed into different employee types (`HourlyEmployee`, `SalariedEmployee`, `Freelancer`). While this separation might initially seem logical, the design becomes increasingly complex when introducing new features, like commission. This complexity often results in a proliferation of subclasses and repetitive code.

On the other hand, the composition paradigm showcases a design pattern where employee types and features are treated as separate modular entities. This approach prevents redundancy and provides the flexibility to add or modify features independently.

## Files in the Repository

1. **Inheritance.py**: Demonstrates the inheritance approach to manage employees.
2. **Composition.py**: Illustrates the composition technique for a more modular design.

## Code Snippets

**Inheritance Approach**

```python
@dataclass
class SalariedEmployeeWithCommission(SalariedEmployee):
    """Employee that's paid based on a fixed monthly salary and that gets a commission."""

    commission: float = 100
    contracts_landed: float = 0

    def compute_pay(self) -> float:
        return super().compute_pay() + self.commission * self.contracts_landed
```

**Composition Approach**

```python
@dataclass
class Employee:
    """Basic representation of an employee at the company."""

    name: str
    id: int
    contract: Contract
    commission: Optional[Commission] = None

    def compute_pay(self) -> float:
        """Compute how much the employee should be paid."""
        payout = self.contract.get_payment()
        if self.commission is not None:
            payout += self.commission.get_payment()
        return payout
```

## Running the Code

To run the provided examples, execute the respective python files:

```bash
$ python Inheritance.py
$ python Composition.py
```

## Conclusion

By comparing the two paradigms side-by-side, it becomes evident that while inheritance is intuitive for some hierarchical structures, it can become complex and rigid. Composition, with its modular approach, offers a more scalable and maintainable system, especially when frequent changes or extensions are expected.

---

You can now use this README as a guide for anyone diving into your repository!