# Deleting a cloud network

{% note alert %}

Before you delete a network, you need to [delete](subnet-delete.md) all its subnets.

You cannot restore a network after it is deleted.

{% endnote %}

{% list tabs %}

- Management console

   To delete a [cloud network](../concepts/network.md#network):
   1. In the [management console]({{ link-console-main }}), go to the folder where you need to delete a cloud network.
   1. In the list of services, select **{{ vpc-name }}**.
   1. Click ![image](../../_assets/options.svg) in the line of the network to delete.
   1. In the menu that opens, click **Delete**.
   1. In the window that opens, click **Delete**.

- CLI

   {% include [include](../../_includes/cli-install.md) %}

   {% include [default-catalogue](../../_includes/default-catalogue.md) %}

   1. See the description of the CLI's delete cloud network command:

      ```
      yc vpc network delete --help
      ```

   1. Get a list of all networks in the default folder:

      ```
      yc vpc network list
      ```

      Result:
      ```
      +----------------------+----------------+
      |          ID          |      NAME      |
      +----------------------+----------------+
      | enpiuvhhd4t80k4n80i8 | test-network-1 |
      | enplom7a98s1t0lhass8 | default        |
      +----------------------+----------------+
      ```

   1. Select the `ID` or `NAME` of the network you need.
   1. Delete the network:

      ```
      yc vpc network delete test-network-1
      ```

- {{ TF }}

   For more information about the {{ TF }}, [see the documentation](../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform).

   {% include [terraform-definition](../../_tutorials/terraform-definition.md) %}

   To delete a cloud network created with {{ TF }}:

   1. Open the {{ TF }} configuration file and delete the fragment with the cloud network description.

      {% cut "Example cloud network description in a {{ TF }} configuration" %}

      ```hcl
      ...
      resource "yandex_vpc_network" "default" {
        name        = "network-1"
        description = "My first network"
        labels = {
          tf-label    = "tf-label-value"
          empty-label = ""
        }
      }
      ...
      ```

      {% endcut %}

   1. In the command line, go to the directory with the {{ TF }} configuration file.

   1. Check the configuration using the command:

      ```
      terraform validate
      ```

      If the configuration is correct, the following message is returned:

      ```
      Success! The configuration is valid.
      ```

   1. Run the command:

      ```
      terraform plan
      ```

      The terminal will display a list of resources with parameters. No changes are made at this step. If the configuration contains errors, {{ TF }} will point them out.

   1. Apply the configuration changes:

      ```
      terraform apply
      ```

   1. Confirm the changes: type `yes` into the terminal and press **Enter**.

      You can verify the changes using the [management console]({{ link-console-main }}) or the [CLI](../../cli/quickstart.md) command below:

      ```
      yc vpc network list
      ```

{% endlist %}
