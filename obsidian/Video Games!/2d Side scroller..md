

Make a 2d Platformer game where your goal is to keep moving right will a constant wall of death moving to the right. Make it have multiple weapons and Cool bosses that you have to defeat in cool ways before the wall of death to the left gets you. Using GODOT engine. Im starting this today.

- Implement a slamming mechanic that if you slam on a enemy it will kill them but if you slam on a tile it will shatter it. 
- Also make Certain gun bullets shatter Tiles/Platforms in the game I think ill implement this by making an if statement and if something is of a high enough velocity it will shatter the platform and the only things with that high velocity will be bullets/slams


extends CharacterBody2D


const SPEED = 300.0
const JUMP_VELOCITY = -400.0


func _physics_process(delta: float) -> void:
	# Add the gravity.
	if not is_on_floor():
		velocity += get_gravity() * delta

	# Handle jump.
	if Input.is_action_just_pressed("ui_accept") and is_on_floor():
		velocity.y = JUMP_VELOCITY

	# Get the input direction and handle the movement/deceleration.
	# As good practice, you should replace UI actions with custom gameplay actions.
	var direction := Input.get_axis("ui_left", "ui_right")
	if direction:
		velocity.x = direction * SPEED
	else:
		velocity.x = move_toward(velocity.x, 0, SPEED)

	move_and_slide()
