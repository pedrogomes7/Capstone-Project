# Capstone Project

## I. Project overview
The project overall idea is to manage the water stock from a facility/ business/ service, in this case the water management of a farm.
This water stock would be only a single storage element, let's say a huge tank, so that it could be reduced the complexity of the current project.

The project integrates four templates : 
- **FarmWaterStock**, the contract that will be holding the information about how much water would be being stored;
- **AddWaterRequest**, a proposal/ request contract that will have the information for the water amount to be requested to a supplier (accepted later on by the manager to not add up complexity);
- **ConsumeWaterRequest**, a proposal/ request contract that will have the information for the water amount consumed in any farm operation;
- **RejectedRequest**, the contract that holds information about any request/ proposal being rejected including a description and the operation type (water request or water consumption).

Parties involved : 
- **Manager**, the party that is in charge of the farm management and accepts/ rejects proposals;
- **Employee**, the party that can propose a operation inside the farm and also has visibility on what's happening at the farm (on the contracts);
- **Supervisor**, the party that only has visibility over the contracts but never participates in any other way.


## II. Project Flow
- The manager creates a **FarmWaterStock** contract with employee and supervisor as observers, a water quantity and some other fields.

- In case that the employee sees fit to propose a request of more water(quantity) he can do so by exercising the choice **RequestAddWater**. This choice takes a supplier field(this field is just a text field that records a supplier name, nothing else was implemented to not add up complexity) and the quantity that he sees fit and it creates a **AddWaterRequest** contract. After it :
    - The request can then be approved by the manager by exercising **AcceptAddWaterRequest**. This acceptance choice would create a new **FarmWaterStock** contract with the new water amount(quantity) and archive the previous one;
    - Otherwise the manager can reject the Request by exercising the choice **RejectAddWaterRequest** that will create a **RejectedRequest** contract.

- When it's time to update log the water consumption the employee can request the water consumption so that the manager can analyze it and accept/ reject it. The request is done by the employee exercising the choice **WaterConsumptionRequest**, creating a **ConsumeWaterRequest** contract that can : 
    - Be accepted by the manager by exercising **AcceptWaterConsuption**. This acceptance choice would create a new **FarmWaterStock** contract with the new water amount(quantity) and consuming previous one;
    - Be rejected by the manager by exercising the choice **RejectWaterConsuption** that will create a **RejectedRequest** contract when provided with a reason.

- The manager can also exercise straight forward the choice **ConsumeWater** that creates a new **FarmWaterStock** contract with the new water amount(quantity) and consumes previous one;

- It is possible for the employees to revoke the requests by exercising **RevokeAddWaterRequest** and **RevokeConsumeWaterRequest**, this exercise will consume the contracts and ending up "revoking" them.


## III. How to run the system

### Daml Studio
Daml Studio can be started by running command `daml studio ` when inside the project folder.

### Build
The project can be built by running command ` daml build `.

### Clean
The project built artifacts can be cleaned by running command ` daml clean `.

### Daml Sandbox
Daml Sandbox can be started by running command ` daml start `.
