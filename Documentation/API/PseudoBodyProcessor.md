# Class PseudoBodyProcessor

Sets up the PseudoBody prefab based on the provided user settings and implements the logic to represent a body.

## Contents

* [Inheritance]
* [Namespace]
* [Syntax]
* [Fields]
  * [collisionResolutionMovement]
  * [ignoredColliders]
  * [ignoreInteractorCollisions]
  * [offsetObjectFollower]
  * [previousRigidbodyPosition]
  * [restoreColliders]
  * [rigidbodySetFrameCount]
  * [sourceObjectFollower]
  * [wasCharacterControllerGrounded]
  * [wasDiverged]
* [Properties]
  * [Character]
  * [CollisionsToIgnore]
  * [Facade]
  * [Interest]
  * [IsCharacterControllerGrounded]
  * [IsDiverged]
  * [PhysicsBody]
  * [RigidbodyCollider]
* [Methods]
  * [Awake()]
  * [CheckDivergence()]
  * [CheckIfCharacterControllerIsGrounded()]
  * [ConfigureOffsetObjectFollower()]
  * [ConfigureSourceObjectFollower()]
  * [EmitIsGroundedChangedEvent(Boolean)]
  * [IgnoreInteractorGrabbedCollision(InteractableFacade)]
  * [IgnoreInteractorsCollisions(InteractorFacade)]
  * [MatchCharacterControllerWithSource(Boolean)]
  * [MatchRigidbodyAndColliderWithCharacterController()]
  * [OnAfterInterestChange()]
  * [OnDisable()]
  * [OnEnable()]
  * [Process()]
  * [RememberCurrentPositions()]
  * [ResumeInteractorsCollisions(InteractorFacade)]
  * [ResumeInteractorUngrabbedCollision(InteractableFacade)]
  * [SolveBodyCollisions()]
* [Implements]

## Details

##### Inheritance

* System.Object
* PseudoBodyProcessor

##### Implements

IProcessable

##### Namespace

* [Tilia.Trackers.PseudoBody]

##### Syntax

```
public class PseudoBodyProcessor : MonoBehaviour, IProcessable
```

### Fields

#### collisionResolutionMovement

Movement to apply to [Character] to resolve collisions.

##### Declaration

```
protected static readonly Vector3 collisionResolutionMovement
```

#### ignoredColliders

The colliders to ignore body collisions with.

##### Declaration

```
protected readonly HashSet<Collider> ignoredColliders
```

#### ignoreInteractorCollisions

Stores the routine for ignoring interactor collisions.

##### Declaration

```
protected Coroutine ignoreInteractorCollisions
```

#### offsetObjectFollower

An optional follower of [Offset].

##### Declaration

```
protected ObjectFollower offsetObjectFollower
```

#### previousRigidbodyPosition

The previous position of [PhysicsBody].

##### Declaration

```
protected Vector3 previousRigidbodyPosition
```

#### restoreColliders

The colliders to restore after an ungrab.

##### Declaration

```
protected readonly HashSet<Collider> restoreColliders
```

#### rigidbodySetFrameCount

The frame count of the last time [Interest] was set to [Rigidbody] or [RigidbodyUntilGrounded].

##### Declaration

```
protected int rigidbodySetFrameCount
```

#### sourceObjectFollower

An optional follower of [Source].

##### Declaration

```
protected ObjectFollower sourceObjectFollower
```

#### wasCharacterControllerGrounded

Whether [Character] was grounded previously.

##### Declaration

```
protected bool? wasCharacterControllerGrounded
```

#### wasDiverged

Whether Facade.Source was previously diverged from the [Character].

##### Declaration

```
protected bool wasDiverged
```

### Properties

#### Character

The UnityEngine.CharacterController that acts as the main representation of the body.

##### Declaration

```
public CharacterController Character { get; protected set; }
```

#### CollisionsToIgnore

A CollisionIgnorer to manage ignoring collisions with the PseudoBody colliders.

##### Declaration

```
public CollisionIgnorer CollisionsToIgnore { get; protected set; }
```

#### Facade

The public interface facade.

##### Declaration

```
public PseudoBodyFacade Facade { get; protected set; }
```

#### Interest

The object that defines the main source of truth for movement.

##### Declaration

```
public PseudoBodyProcessor.MovementInterest Interest { get; set; }
```

#### IsCharacterControllerGrounded

Whether [Character] touches ground.

##### Declaration

```
public bool IsCharacterControllerGrounded { get; }
```

#### IsDiverged

Whether Facade.Source has diverged from the [Character].

##### Declaration

```
public bool IsDiverged { get; protected set; }
```

#### PhysicsBody

The Rigidbody that acts as the physical representation of the body.

##### Declaration

```
public Rigidbody PhysicsBody { get; protected set; }
```

#### RigidbodyCollider

The CapsuleCollider that acts as the physical collider representation of the body.

##### Declaration

```
public CapsuleCollider RigidbodyCollider { get; protected set; }
```

### Methods

#### Awake()

##### Declaration

```
protected virtual void Awake()
```

#### CheckDivergence()

Check to see if the Facade.Source has diverged or converged with the [Character].

##### Declaration

```
protected virtual void CheckDivergence()
```

#### CheckIfCharacterControllerIsGrounded()

Checks whether [Character] is grounded.

##### Declaration

```
protected virtual bool CheckIfCharacterControllerIsGrounded()
```

##### Returns

| Type | Description |
| --- | --- |
| System.Boolean | Whether [Character] is grounded. |

##### Remarks

CharacterController.isGrounded isn't accurate so this method does an additional check using Physics.

#### ConfigureOffsetObjectFollower()

Configures the offset object follower based on the facade settings.

##### Declaration

```
public virtual void ConfigureOffsetObjectFollower()
```

#### ConfigureSourceObjectFollower()

Configures the source object follower based on the facade settings.

##### Declaration

```
public virtual void ConfigureSourceObjectFollower()
```

#### EmitIsGroundedChangedEvent(Boolean)

Emits BodyRepresentationFacade.BecameGrounded or [BecameAirborne].

##### Declaration

```
protected virtual void EmitIsGroundedChangedEvent(bool isCharacterControllerGrounded)
```

##### Parameters

| Type | Name | Description |
| --- | --- | --- |
| System.Boolean | isCharacterControllerGrounded | The current state. |

#### IgnoreInteractorGrabbedCollision(InteractableFacade)

Ignores the interactable grabbed by the interactor.

##### Declaration

```
protected virtual void IgnoreInteractorGrabbedCollision(InteractableFacade interactable)
```

##### Parameters

| Type | Name | Description |
| --- | --- | --- |
| InteractableFacade | interactable | The interactable to ignore. |

#### IgnoreInteractorsCollisions(InteractorFacade)

Ignores all of the colliders on the interactor collection.

##### Declaration

```
public virtual void IgnoreInteractorsCollisions(InteractorFacade interactor)
```

##### Parameters

| Type | Name | Description |
| --- | --- | --- |
| InteractorFacade | interactor | n/a |

#### MatchCharacterControllerWithSource(Boolean)

Changes the height and position of [Character] to match [Source].

##### Declaration

```
protected virtual void MatchCharacterControllerWithSource(bool setPositionDirectly)
```

##### Parameters

| Type | Name | Description |
| --- | --- | --- |
| System.Boolean | setPositionDirectly | Whether to set the position directly or tell [Character] to move to it. |

#### MatchRigidbodyAndColliderWithCharacterController()

Changes [RigidbodyCollider] to match the collider settings of [Character] and moves [PhysicsBody] to match [Character].

##### Declaration

```
protected virtual void MatchRigidbodyAndColliderWithCharacterController()
```

#### OnAfterInterestChange()

Called after [Interest] has been changed.

##### Declaration

```
protected virtual void OnAfterInterestChange()
```

#### OnDisable()

##### Declaration

```
protected virtual void OnDisable()
```

#### OnEnable()

##### Declaration

```
protected virtual void OnEnable()
```

#### Process()

Positions, sizes and controls all variables necessary to make a body representation follow the given [Source].

##### Declaration

```
public virtual void Process()
```

#### RememberCurrentPositions()

Updates the previous position variables to remember the current state.

##### Declaration

```
protected virtual void RememberCurrentPositions()
```

#### ResumeInteractorsCollisions(InteractorFacade)

Resumes all of the colliders on the interactor collection.

##### Declaration

```
public virtual void ResumeInteractorsCollisions(InteractorFacade interactor)
```

##### Parameters

| Type | Name | Description |
| --- | --- | --- |
| InteractorFacade | interactor | n/a |

#### ResumeInteractorUngrabbedCollision(InteractableFacade)

Resumes the interactable ungrabbed by the interactor.

##### Declaration

```
protected virtual void ResumeInteractorUngrabbedCollision(InteractableFacade interactable)
```

##### Parameters

| Type | Name | Description |
| --- | --- | --- |
| InteractableFacade | interactable | The interactable to resume. |

#### SolveBodyCollisions()

Solves body collisions by not moving the body in case it can't go to its current position.

##### Declaration

```
public virtual void SolveBodyCollisions()
```

##### Remarks

If body collisions should be prevented this method needs to be called right before or right after applying any form of movement to the body.

### Implements

IProcessable

[Tilia.Trackers.PseudoBody]: README.md
[Character]: PseudoBodyProcessor.md#Character
[Offset]: PseudoBodyFacade.md#Tilia_Trackers_PseudoBody_PseudoBodyFacade_Offset
[PhysicsBody]: PseudoBodyProcessor.md#PhysicsBody
[Interest]: PseudoBodyProcessor.md#Interest
[Rigidbody]: PseudoBodyProcessor.MovementInterest.md#MovementInterest_Rigidbody
[RigidbodyUntilGrounded]: PseudoBodyProcessor.MovementInterest.md#MovementInterest_RigidbodyUntilGrounded
[Source]: PseudoBodyFacade.md#Tilia_Trackers_PseudoBody_PseudoBodyFacade_Source
[Character]: PseudoBodyProcessor.md#Character
[Character]: PseudoBodyProcessor.md#Character
[PseudoBodyFacade]: PseudoBodyFacade.md
[PseudoBodyProcessor.MovementInterest]: PseudoBodyProcessor.MovementInterest.md
[Character]: PseudoBodyProcessor.md#Character
[Character]: PseudoBodyProcessor.md#Character
[Character]: PseudoBodyProcessor.md#Character
[Character]: PseudoBodyProcessor.md#Character
[Character]: PseudoBodyProcessor.md#Character
[BecameAirborne]: PseudoBodyFacade.md#Tilia_Trackers_PseudoBody_PseudoBodyFacade_BecameAirborne
[Character]: PseudoBodyProcessor.md#Character
[Source]: PseudoBodyFacade.md#Tilia_Trackers_PseudoBody_PseudoBodyFacade_Source
[Character]: PseudoBodyProcessor.md#Character
[RigidbodyCollider]: PseudoBodyProcessor.md#RigidbodyCollider
[Character]: PseudoBodyProcessor.md#Character
[PhysicsBody]: PseudoBodyProcessor.md#PhysicsBody
[Character]: PseudoBodyProcessor.md#Character
[Interest]: PseudoBodyProcessor.md#Interest
[Source]: PseudoBodyFacade.md#Tilia_Trackers_PseudoBody_PseudoBodyFacade_Source
[Inheritance]: #Inheritance
[Namespace]: #Namespace
[Syntax]: #Syntax
[Fields]: #Fields
[collisionResolutionMovement]: #collisionResolutionMovement
[ignoredColliders]: #ignoredColliders
[ignoreInteractorCollisions]: #ignoreInteractorCollisions
[offsetObjectFollower]: #offsetObjectFollower
[previousRigidbodyPosition]: #previousRigidbodyPosition
[restoreColliders]: #restoreColliders
[rigidbodySetFrameCount]: #rigidbodySetFrameCount
[sourceObjectFollower]: #sourceObjectFollower
[wasCharacterControllerGrounded]: #wasCharacterControllerGrounded
[wasDiverged]: #wasDiverged
[Properties]: #Properties
[Character]: #Character
[CollisionsToIgnore]: #CollisionsToIgnore
[Facade]: #Facade
[Interest]: #Interest
[IsCharacterControllerGrounded]: #IsCharacterControllerGrounded
[IsDiverged]: #IsDiverged
[PhysicsBody]: #PhysicsBody
[RigidbodyCollider]: #RigidbodyCollider
[Methods]: #Methods
[Awake()]: #Awake
[CheckDivergence()]: #CheckDivergence
[CheckIfCharacterControllerIsGrounded()]: #CheckIfCharacterControllerIsGrounded
[ConfigureOffsetObjectFollower()]: #ConfigureOffsetObjectFollower
[ConfigureSourceObjectFollower()]: #ConfigureSourceObjectFollower
[EmitIsGroundedChangedEvent(Boolean)]: #EmitIsGroundedChangedEventBoolean
[IgnoreInteractorGrabbedCollision(InteractableFacade)]: #IgnoreInteractorGrabbedCollisionInteractableFacade
[IgnoreInteractorsCollisions(InteractorFacade)]: #IgnoreInteractorsCollisionsInteractorFacade
[MatchCharacterControllerWithSource(Boolean)]: #MatchCharacterControllerWithSourceBoolean
[MatchRigidbodyAndColliderWithCharacterController()]: #MatchRigidbodyAndColliderWithCharacterController
[OnAfterInterestChange()]: #OnAfterInterestChange
[OnDisable()]: #OnDisable
[OnEnable()]: #OnEnable
[Process()]: #Process
[RememberCurrentPositions()]: #RememberCurrentPositions
[ResumeInteractorsCollisions(InteractorFacade)]: #ResumeInteractorsCollisionsInteractorFacade
[ResumeInteractorUngrabbedCollision(InteractableFacade)]: #ResumeInteractorUngrabbedCollisionInteractableFacade
[SolveBodyCollisions()]: #SolveBodyCollisions
[Implements]: #Implements
