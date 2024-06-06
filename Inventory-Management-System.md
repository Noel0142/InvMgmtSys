# INVENTORY MANAGEMENT SYSTEM

## Table of Contents
- [INVENTORY MANAGEMENT SYSTEM](#inventory-management-system)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Tools and Technologies Used](#tools-and-technologies-used)
  - [Setting Up Notion Database](#setting-up-notion-database)
  - [Configuring Zapier Integration](#configuring-zapier-integration)
  - [Testing the Automation](#testing-the-automation)
  - [Advanced Concepts and Techniques](#advanced-concepts-and-techniques)
    <!-- - [Webhooks](#webhooks)
    - [Conditional Logic](#conditional-logic)
    - [Concepts and Skills Developed](#concepts-and-skills-developed) -->
  - [Conclusion](#conclusion)


## Overview
Utilizing Zapier to automate email notifications and Notion to create an inventory management system. The intention was to make sure that, in the event that a stock amount drops to zero, an automated email informing the administrator to replenish supplies would be issued.

## Tools and Technologies Used
- **Notion**: For creating and managing the inventory database.
- **Zapier**: For automating the workflow and sending email notifications.
- **Gmail**: For sending emails (can be replaced with any email service).
- **VS Code**: For documentation.

## Setting Up Notion Database
   ### 1. Set up a Notion database with the following fields:
   - **Item Description**: Name of the inventory item.
   - **Stock Capacity**: Number of items in stock.
   - **Stock Used**:Quantity of stock items that have been consumed or utilized.
   - **Current Stock**:Quantity of stock items currently available in inventory.
   - **Reorder Level**:Minimum quantity of stock at which new items should be ordered to maintain inventory levels.
   - **Stock Alert**: Formulas to generate a stock alert message.
   - **Unit Type**:The standard measurement or classification for a particular item or product.
   - **Employee Remarks**:Comments or notes made by employees regarding a specific issue, task, or observation.
  
  ![Inventory Management System Home Page](./assets/Inventory%20Management%20System%20Home%20Page.png)
  ![Inventory Management System Page 1](./assets/Inventory%20Management%20System%20Page%201.png)
  <!-- ![Inventory Management System Page 2](./assets/Inventory%20Management%20System%20Page%202.png) -->

   ### 2. Formula for Stock Alert
   ```notion
    if(prop("Current Stock") == 0, 
    "🚨 Stock quantity is zero. Immediate restock required.", 
    if(prop("Current Stock") <= prop("Reorder Level"), 
        "🔴 Low Stock. Restock soon.",
        if(prop("Current Stock") <= (prop("Reorder Level") + 5), 
            "🟡 Moderate Stock. Consider restocking.", 
            "✅ Stock level is sufficient."
          )
        )
      )  
   ```

## Configuring Zapier Integration
   ### 1. Create a New Zap
   - **Trigger**: "Updated Database Item in Notion"
     - Choose the Notion database you created.
   - **Filter**: "Only Continue If..."
     - Set up the filter to check the "Current Stock" field.
     - Condition: (Number) Less than
     - Value: 1

   ### 2. Action
   - **Send Email via Gmail**:
       - Configure the email action to send a notification to the admin.
       - Customize the email content to include the item details.

  ![Zapier Email Setup 1](./assets/Zapier%20Email%20Setup%201.jpeg)
    
  ![Zapier Email Setup 2](./assets/Zapier%20Email%20Setup%202.png)
    
  ![Zapier Email Setup 3](./assets/Zapier%20Email%20Setup%203.png)

  ![Email Notification Example](./assets/Email%20Notification%20Example.png)

## Testing the Automation
   ### 1. Update a Test Item in Notion
   - Set the stock quantity of a test item to zero.
   - Verify that the stock alert message updates correctly.

   ### 2. Test the Zap
   - Manually trigger the Zap in Zapier using the test item.
   - Check the task history to ensure it passed the filter and sent the email.
   - Verify receipt of the email in the admin's inbox.

   ![Zapier Task](./assets/Zapier%20Task.png)

## Advanced Concepts and Techniques
<!-- ### Webhooks
- **Understanding Webhooks**: Webhooks allow applications to send real-time data to other services. They provide a way for one application to notify another when an event has occurred, making them ideal for scenarios where immediate action is required.
- **Setting Up Webhooks in Zapier**:
  1. **Trigger via Webhook**: Instead of polling for changes at regular intervals, webhooks enable Notion (if supported) or another intermediary service to push data to Zapier instantly when inventory updates occur.
  2. **Webhook Action**: Configure the webhook to send inventory data changes directly to Zapier. Zapier can then process this data and trigger subsequent actions, such as sending an email alert.

### Conditional Logic
- **Understanding Conditional Logic**: Conditional logic allows the creation of dynamic workflows that only proceed when certain conditions are met. This is useful for ensuring actions are only taken when necessary.
- **Implementing Conditional Logic in Zapier**:
  - Use filters to set conditions based on Notion data fields.
  - Combine multiple conditions using logical operators (ONLY IF, AND, OR).

## Concepts
Throughout this project, I developed and refined several key skills and concepts:

- **Database Management in Notion**: The setup and management of dynamic databases, including the use of formulas to generate alerts.
- **Automation with Zapier**: Creating automated workflows to integrate different apps and services seamlessly.
- **Conditional Logic**: Utilizing Zapier's filters and Notion's formulas to create conditional workflows based on specific criteria.
- **Webhooks**: Understanding the role of webhooks in real-time data synchronization and how to implement them for immediate data updates and automation.
- **Testing and Debugging**: Conducted thorough testing and troubleshooting to ensure smooth workflow operations.
- **Real-Time Data Management**: Leveraged webhooks to maintain up-to-date information across systems, ensuring accurate data reflection across platforms.
- **Cross-Application Integration**: Learnt how to efficiently integrate multiple applications (Notion and Gmail) via Zapier, understanding data flows between these platforms, and how to manage these integrations efficiently. -->
### 1. Webhooks

**Understanding Webhooks**:  
Webhooks allow applications to send real-time data to other services. They provide a way for one application to notify another when an event has occurred, making them ideal for scenarios where immediate action is required.

#### Setting Up Webhooks in Zapier
- **Trigger via Webhook**: Instead of polling for changes at regular intervals, webhooks enable Notion (if supported) or another intermediary service to push data to Zapier instantly when inventory updates occur.
- **Webhook Action**: Configure the webhook to send inventory data changes directly to Zapier. Zapier can then process this data and trigger subsequent actions, such as sending an email alert.

### 2. Conditional Logic

**Understanding Conditional Logic**:  
Conditional logic allows the creation of dynamic workflows that only proceed when certain conditions are met. This is useful for ensuring actions are only taken when necessary.

#### Implementing Conditional Logic in Zapier
- Use filters to set conditions based on Notion data fields.
- Combine multiple conditions using logical operators (ONLY IF, AND, OR).

### 3. Concepts and Skills Developed

Throughout this project, I developed and refined several key skills and concepts:

**Database Management in Notion**:
- The setup and management of dynamic databases, including the use of formulas to generate alerts.

**Automation with Zapier**:
- Creating automated workflows to integrate different apps and services seamlessly.

**Conditional Logic**:
- Utilizing Zapier's filters and Notion's formulas to create conditional workflows based on specific criteria.

**Webhooks**:
- Understanding the role of webhooks in real-time data synchronization and how to implement them for immediate data updates and automation.

**Testing and Debugging**:
- Conducted thorough testing and troubleshooting to ensure smooth workflow operations.

**Real-Time Data Management**:
- Leveraged webhooks to maintain up-to-date information across systems, ensuring accurate data reflection across platforms.

**Cross-Application Integration**:
- Learned how to efficiently integrate multiple applications (Notion and Gmail) via Zapier, understanding data flows between these platforms, and how to manage these integrations efficiently.

## Conclusion
This project demonstrated how to leverage Notion and Zapier to create an automated inventory management system. It provided valuable experience in integrating different tools to streamline processes and ensure efficient management of inventory levels. The use of webhooks added an advanced layer of real-time data handling, making the system more responsive and efficient. Future enhancements could include additional automation features and integration with other inventory management tools.


 