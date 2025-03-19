March 12
csharp
코드 복사
using UnityEngine.SceneManagement; // Required to use LoadScene()

if (Input.GetMouseButtonDown(0))
{
    SceneManager.LoadScene("GameScene");
}
Touching the screen transitions to the Game Scene.
In Build Settings, scenes must be registered and ordered starting from index 0 in the Scene List.
csharp
코드 복사
// Restart from the beginning if the player goes off-screen
if (transform.position.y < -10)
{
    SceneManager.LoadScene("GameScene");
}
If mistakenly set to 10 instead of -10, the game continuously restarts because the player’s initial position is below 10.
Animation
In Animator Window, under the Parameters tab (top left), click + to add a Trigger, set its name, and assign it to a transition arrow under Conditions.
In the script, trigger activation on jumping:
csharp
코드 복사
// Jump
if (Input.GetMouseButtonDown(0) && this.rigid2D.linearVelocity.y == 0)
{
    this.animator.SetTrigger("JumpTrigger");
    this.rigid2D.AddForce(transform.up * this.jumpForce);
}
Forgot I changed the jump key to mouse click and kept pressing the spacebar → Failed
March 13
Scene Gizmo: Used to check screen orientation.
Terrain: A prebuilt terrain object in Unity.
March 14
Terrain Brush Functionality
Python Code
python
코드 복사
my_list = ["apple", "banana", "cherry"]
user_input = input("Enter a fruit: ")

if user_input in my_list:
    print("Exists in the list")
else:
    print("Not in the list")
March 15
Python: Ramen Cooking Simulator
python
코드 복사
while True:
    print(f"\nWelcome to the Ramen Cooking Simulator (Python Version)!\n")
    ingredients = ["Water", "Noodles", "Soup Base", "Green Onion", "Egg", "Flakes"]
    print(f"Ingredients and pot are ready!")
    print(f"Remaining ingredients: {ingredients}")
    used = []  # List to store first selected ingredient

    choice = input("\nWhich ingredient will you add first? ")
    used.append(choice)

    if used[0] != ingredients[0]:
        print(f"Oh no! You must add water first!\n")
        print(f"Restarting from the beginning!\n")
        continue
    else:
        print(f"%s has been added!" % (choice))
        ingredients.remove(choice)
        print(f"\nRemaining ingredients: {ingredients}")
        
        while True:
            if len(ingredients) == 0:
                print(f"\nAll ingredients have been used!")
                print(f"Ramen Cooking Simulator is ending. Enjoy your ramen!")
                break
                
            ingre_choice = input("\nWhat ingredient will you add next? ")

            if ingre_choice in ingredients:
                ingredients.remove(ingre_choice)
                print(f"%s has been added!" % (ingre_choice))
                print(f"\nRemaining ingredients: {ingredients}")

                continue_or_break = input("Would you like to add another ingredient? [Y/N] ")
                if continue_or_break.lower() == 'y':
                    continue
                elif continue_or_break.lower() == 'n':
                    print(f"\nEnding the Ramen Cooking Simulator. Enjoy your meal!")
                    break
                else:
                    print(f"Invalid response!")
                    break
            else:
                print(f"This ingredient does not exist!")
                break
March 16
csharp
코드 복사
Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
Vector3 worldDir = ray.direction;
bamsongi.GetComponent<BamsongiController>().Shoot(worldDir.normalized * 2000);
March 17
Baking: Precomputing light and shadow information caused by lights and embedding it into textures to reduce runtime processing load.
March 18
csharp
코드 복사
if (Input.GetMouseButtonDown(0))
{
    Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
    RaycastHit hit;
    if (Physics.Raycast(ray, out hit, Mathf.Infinity))
    {
        float x = Mathf.RoundToInt(hit.point.x);
        float z = Mathf.RoundToInt(hit.point.z);
        transform.position = new Vector3(x, 0, z);
    }
}
March 19
csharp
코드 복사
public class ItemController : MonoBehaviour
{
    public float dropSpeed = -0.03f; // Falling speed

    void Update()
    {
        transform.Translate(0, this.dropSpeed, 0); 
        if (transform.position.y < -1.0f)
        {
            Destroy(gameObject);
        }
    }
}
Collision Mode: Detects collision and reacts physically.
Trigger Mode: Only detects collision; the colliding object passes through.
The colliding object is passed as a parameter to OnTriggerEnter(Collider other).
✔ OnTriggerEnter(Collider other) is an event-based function in Unity and does not need to be inside Update().
✔ Unity automatically calls this function when a collision is detected, so there is no need to manually check for collisions in Update().

General C# Methods
✔ A general C# method is one that Unity does not automatically call; it must be manually executed.
✔ Inside a MonoBehaviour class, you can define regular C# methods, but they must be explicitly called to run.
