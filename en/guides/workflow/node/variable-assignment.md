# Variable Assigner

### Definition

The variable assigner node is used to assign values to writable variables. Currently supported writable variables include:

- [Session variables](../key_concept.md#session-variables).

Usage: Through the variable assigner node, you can assign workflow variables to session variables for temporary storage, which can be continuously referenced in subsequent conversations.

<figure><img src="../../../../img/variable-assigner.png" alt="" width="375"><figcaption></figcaption></figure>

***

### Usage Scenario Examples

Using the variable assigner node, you can write context from the conversation process, files uploaded to the dialog box (coming soon), and user preference information into session variables. These stored variables can then be referenced in subsequent conversations to direct different processing flows or formulate responses.

**Scenario 1**

**Recording initial user preferences**: Remember the user's language preference input during the conversation and continue to use this language type for responses in subsequent dialogues.

Example: Before the conversation begins, the user specifies "English" in the `language` input box. This language will be written to the session variable, and the LLM will reference this information when responding, continuing to use "English" in subsequent conversations.

<figure><img src="../../../../img/conversation-var-scenario-1.png" alt=""><figcaption></figcaption></figure>

**Configuration Process:**

**Set session variable**: First, set a session variable `language`. Add a condition judgment node at the beginning of the conversation flow to check if the `language` variable is empty.

**Variable writing/assignment**: At the start of the first round of dialogue, if the `language` variable is empty, use an LLM node to extract the user's input language, then use a variable assigner node to write this language type into the session variable `language`.

**Variable reading**: In subsequent conversation rounds, the `language` variable has stored the user's language preference. The LLM node references the language variable to respond using the user's preferred language type.

**Scenario 2**

**Assisting with Checklist checks**: Record user inputs within the conversation using session variables, update the contents of the Checklist, and check for missing items in subsequent conversations.

<figure><img src="../../../../img/conversation-var-scenario-2.png" alt=""><figcaption></figcaption></figure>

Example: After starting the conversation, the LLM will ask the user to input items related to the Checklist in the dialog box. Once the user mentions content from the Checklist, it will be updated and stored in the session variable. The LLM will remind the user to continue supplementing missing items after each round of dialogue.

<figure><img src="../../../../img/conversation-var-scenario-2-1.png" alt=""><figcaption></figcaption></figure>

**Configuration Process:**

* **Set session variable:** First, set a session variable `ai_checklist`, and reference this variable within the LLM as context for checking.
* **variable assigner/writing**: During each round of dialogue, check the value in `ai_checklist` within the LLM node and compare it with user input. If the user provides new information, update the Checklist and write the output content to `ai_checklist` using the variable assigner node.
* **Variable reading:** Read the value in `ai_checklist` and compare it with user input in each round of dialogue until all checklist items are completed.

***

### Using the variable assigner Node

Click the + sign on the right side of the node, select the "variable assigner" node, and fill in "Variable to Assign" and "Set Variable".

<figure><img src="../../../../img/language-variable-assigner.png" alt="" width="375"><figcaption></figcaption></figure>

**Setting Variables:**

Variable to Assign: Select the variable to be assigned, i.e., specify the target session variable that needs to be assigned.

Set Variable: Select the variable to assign, i.e., specify the source variable that needs to be converted.

Taking the assignment logic in the above figure as an example: Assign the text output item `Language Recognition/text` from the previous node to the session variable `language`.

**Write Mode:**

* Overwrite: Overwrite the content of the source variable to the target session variable
* Append: When the specified variable is of Array type
* Clear: Clear the content in the target session variable