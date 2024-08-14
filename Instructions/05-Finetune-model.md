---
lab:
    title: 'Fine-tune a language model for chat completion in the Azure AI Studio'
---

# Fine-tune a language model for chat completion in the Azure AI Studio

In this exercise, you'll fine-tune a language model with the Azure AI Studio that you want to use for a custom copilot scenario.

This exercise will take approximately **45** minutes.

## Before you start

To complete this exercise, your Azure subscription must be approved for access to the Azure OpenAI service. Fill in the [registration form](https://learn.microsoft.com/legal/cognitive-services/openai/limited-access) to request access to Azure OpenAI models.

## Create an AI hub and project in the Azure AI Studio

You start by creating an Azure AI Studio project within an Azure AI hub:

1. In a web browser, open [https://ai.azure.com](https://ai.azure.com) and sign in using your Azure credentials.
1. Select the **Home** page, then select **+ New project**.
1. In the **Create a new project** wizard, create a project with the following settings:
    - **Project name**: *A unique name for your project*
    - **Hub**: *Create a new hub with the following settings:*
        - **Hub name**: *A unique name*
        - **Subscription**: *Your Azure subscription*
        - **Resource group**: *A new resource group*
        - **Location**: *Make a **random** choice from any of the following regions*\*
        - East US 2
        - North Central US
        - Sweden Central
        - Switzerland North
    - **Connect Azure AI Services or Azure OpenAI**: *Create a new connection*
    - **Connect Azure AI Search**: Skip connecting

    > \* Azure OpenAI resources are constrained at the tenant level by regional quotas. The listed regions include default quota for the model type(s) used in this exercise. Randomly choosing a region reduces the risk of a single region reaching its quota limit. In the event of a quota limit being reached later in the exercise, there's a possibility you may need to create another resource in a different region. Learn more about [model availability per region](https://learn.microsoft.com/en-us/azure/ai-studio/concepts/fine-tuning-overview#azure-openai-models)

1. Review your configuration and create your project.
1. Wait for your project to be created.

## Fine-tune a GPT-3.5 model

Before you can fine-tune a model, you need a dataset.

1. Save the training dataset as JSONL file locally: https://raw.githubusercontent.com/MicrosoftLearning/mslearn-ai-studio/main/data/travel-finetune.jsonl
1. Navigate to the **Fine-tuning** page under the **Tools** section, using the menu on the left.
1. Select the button to add a new fine-tune model, select the `gpt-35-turbo` model, and select **Confirm**.
1. **Fine-tune** the model using the following configuration:
    - **Model version**: *Select the default version*
    - **Model suffix**: `ft-travel`
    - **Azure OpenAI connection**: *Select the connection that was created when you created your hub*
    - **Training data**: Upload files
    - **Upload file**: Select the JSONL file you downloaded in a previous step.

    > **Tip**: You don't have to wait for the data processing to be completed to continue to the next step.

    - **Validation data**: None
    - **Task parameters**: *Keep the default settings*
1. Finetuning will start and may take some time to complete.

> **Note**: Fine-tuning and deployment can take some time, so you may need to check back periodically to complete the next step.

## Deploy the fine-tuned model

When fine-tuning has successfully completed, you can deploy the model.

1. Select the fine-tuned model. Select the **Metrics** tab and explore the fine-tune metrics.
1. Deploy the fine-tuned model with the following configurations:
    - **Deployment name**: *A unique name for your model, you can use the default*
    - **Deployment type**: Standard
    - **Tokens per Minute Rate Limit (thousands)**: 5K
    - **Content filter**: Default

## Test the fine-tuned model

Now that you deployed your fine-tuned model, you can test the model like you can test any other deployed model.

1. When the deployment is ready, navigate to the fine-tuned model and select **Open in playground**.
1. In the chat window, enter the query `What can you do?`
    Notice that even though you didn't specify the system message to instruct your model to answer travel-related questions, the model already understands what it should focus on.
1. Try with another query like `Where should I go on holiday for my 30th birthday?`

## Delete Azure resources

When you finish exploring the Azure AI Studio, you should delete the resources you’ve created to avoid unnecessary Azure costs.

- Navigate to the [Azure portal](https://portal.azure.com) at `https://portal.azure.com`.
- In the Azure portal, on the **Home** page, select **Resource groups**.
- Select the resource group that you created for this exercise.
- At the top of the **Overview** page for your resource group, select **Delete resource group**.
- Enter the resource group name to confirm you want to delete it, and select **Delete**.
