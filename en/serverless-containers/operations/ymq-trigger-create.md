# Creating a trigger for {{ message-queue-short-name }}

Create a [trigger for a {{ message-queue-full-name }} message queue](../concepts/trigger/ymq-trigger.md) and process the messages using the {{ serverless-containers-name }} [container](../concepts/container.md).

{% note warning %}

* You can only create a trigger for a standard message queue.
* The trigger must be in the same cloud as the queue that messages are read from.
* Only one trigger can be created for each message queue.

{% endnote %}

## Before you begin {#before-begin}

To create a trigger, you need:

* A container that the trigger will launch. If you don't have a container:

   * [Create a container](create.md).
   * [Create a container revision](manage-revision.md#create).

* [Service accounts](../../iam/concepts/users/service-accounts.md) with rights:

   * To invoke a container.
   * To read from the queue the trigger receives messages from.
   * (optional) To write to the [Dead Letter Queue](../../serverless-containers/concepts/dlq.md).

   You can use the same service account or different ones. If you don't have a service account, [create one](../../iam/operations/sa/create.md).

* A message queue that the trigger receives messages from. If you don't have a queue, [create one](../../message-queue/operations/message-queue-new-queue.md).

## Creating a trigger {#trigger-create}

{% include [trigger-time](../../_includes/functions/trigger-time.md) %}

{% list tabs %}

- Management console

   1. In the [management console]({{ link-console-main }}), select the folder where you wish to create your trigger.

   1. Open **{{ serverless-containers-name }}**.

   1. On the left-hand panel, select ![image](../../_assets/functions/triggers.svg) **Triggers**.

   1. Click **Create trigger**.

   1. Under **Basic parameters**:

      * Enter a name and description for the trigger.
      * In the **Type** field, select **{{ message-queue-name }}**.
      * In the **Launched resource** field, select **Container**.

   1. Under **{{ message-queue-name }} settings**, select a message queue and a service account with rights to read messages from this message queue.

   1. (optional) Under **Batch message settings**, specify:

      * Batch size. Values can be from 1 to 10. The default is 1.
      * Maximum wait time. Values can be from 0 to 20 seconds. The default is 10 seconds.

      The trigger groups messages for a period of time not exceeding the specified timeout and sends them to a container. However, the number of messages does not exceed the specified group size.

   1. Under **Container settings**, select a container and specify:

      {% include [container-settings](../../_includes/serverless-containers/container-settings.md) %}

   1. Click **Create trigger**.

{% endlist %}

## Checking the result {#check-result}

{% list tabs %}

- {{ serverless-containers-name }}

   {% include [check-result](../../_includes/serverless-containers/check-result.md) %}

- {{ message-queue-name }}

   Check that the number of enqueued messages is decreasing. To do this, view the queue statistics:

   1. In the [management console]({{ link-console-main }}), open **{{ message-queue-name }}**.
   1. Select the queue that you created the trigger for.
   1. Go to **Monitoring**. View the **Messages in queue** chart.

{% endlist %}

## See also

* [{{ message-queue-name }} trigger that passes messages to the {{ sf-name }} function](../../functions/operations/trigger/ymq-trigger-create.md).
