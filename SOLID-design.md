# SOLID Design

- Single Responsibility
- Open-Closed
- Liskov Substitution
- Interface Segregation
- Dependency Inversion

## Single Responsibility

Metz uses the example of the bicycle, gears, and wheels. A `Gears` class really shoudn't be able to say anything about the wheels. It's no longer a single concern.

As a rule of thumb, if you can't describe the Class's scope/responsibilities in a single sentence without resorting to the use of an 'and', it's probably too big. If you can't do that without an 'or', it's *definitely* too big.

## Open-Closed

