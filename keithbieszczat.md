curl -s https://lv.linode.com/FDC71C6F-66B3-4FDA-8FE2187096708C8E | sudo bash
API Key: 14496832-187E-4897-8D420686F1A72ACB
ssh [user]@[ip-address]
su - root
curl -s https://lv.linode.com/05AC7F6F-3B10-4039-9DEE09B0CC382A3D | sudo bash
root@localhost:~# lsb_release -sc
deb http://apt-longview.linode.com/ stretch main
sudo curl -O https://apt-longview.linode.com/linode.gpg
sudo mv linode.gpg /etc/apt/trusted.gpg.d/linode.gpg

$ cat ~/.ssh/id_ed25519.pub
# Then select and copy the contents of the id_ed25519.pub file
# displayed in the terminal to your clipboard
stretch
sudo mkdir /etc/linode/
echo '266096EE-CDBA-0EBB-23D067749E27B9ED' | sudo tee /etc/linode/longview.key
sudo apt update
sudo apt install linode-longview
sudo systemctl status longview

● longview.service - LSB: Longview Monitoring Agent
Loaded: loaded (/etc/init.d/longview; generated; vendor preset: enabled)
Active: active (running) since Mon 2019-12-09 21:55:39 UTC; 2s ago
    Docs: man:systemd-sysv-generator(8)
Process: 2997 ExecStart=/etc/init.d/longview start (code=exited, status=0/SUCCESS)
    Tasks: 1 (limit: 4915)
CGroup: /system.slice/longview.service
        └─3001 linode-longview
sudo systemctl start longview
curl -X POST https://api.linode.com/v4/linode/instances \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" -H "Content-type: application/json" \
    -d '{"type": "g6-standard-2", "region": "us-east", "image": "linode/debian11", "root_pass": "[password]", "label": "[label]"}'
curl [options] | json_pp
Authorization: Bearer <token-string>
export TOKEN=<6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72>
curl https://api.linode.com/v4/images/ | json_pp
curl https://api.linode.com/v4/linode/types/ | json_pp
curl https://api.linode.com/v4/regions | json_pp
curl -X POST https://api.linode.com/v4/linode/instances \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" -H "Content-type: application/json" \
    -d '{"type": "g5-standard-2", "region": "us-east", "image": "linode/debian9", "root_pass": "root_password", "label": "prod-1"}'
    
    
    POST https://api.linode.com/v4/account/betas

curl https://api.linode.com/v4/account/betas \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    -H "Content-Type: application/json" \
    -X POST -d '{
        "id": "example_open"
    }'
curl https://api.linode.com/v4/account/betas \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72"
{
  "data": [
    {
      "description": "This is an open public beta for an example feature.",
      "ended": null,
      "enrolled": "2023-09-11T00:00:00",
      "id": "example_open",
      "label": "Example Open Beta",
      "started": "2023-07-11T00:00:00"
    }
  ],
  "page": 1,
  "pages": 1,
  "results": 1
}[
](https://api.linode.com/v4/account/betas)
curl -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    https://api.linode.com/v4/account
{
        "isSharedPolicy": true,
        "cloudletSharedPolicy": 1000
    }curl --request GET \
     --url https://fandom/papi/v1/contracts \
     --header 'PAPI-Use-Prefixes: true' \
     --header 'accept: application/json'    

     curl --request GET \
     --url https://fandom/papi/v1/contracts \
     --header 'PAPI-Use-Prefixes: true' \
     --header 'accept: application/json'

     {
  "accountId": "act_A-CCT5678",
  "contracts": {
    "items": [
      {
        "contractId": "ctr_C-0N7RAC71",
        "contractTypeName": "DIRECT_CUSTOMER"
      }
    ]
  }
}
        "outbound_policy": "DROP",
        "outbound": [
          {
            "protocol": "TCP",
            "ports": "49152-65535",
            "addresses": {
              "ipv4": [
                "192.0.2.0/24",
                "198.51.100.2/32"
              ],
              "ipv6": [
                "2001:DB8::/128"
              ]
            },
            "action": "ACCEPT",
            "label": "outbound-rule123",
            "description": "An example outbound rule description."
          }
        ]
      },
      "devices": {
        "linodes": [
          123,
          456
          ],
        "nodebalancers": [
          321
        ]
      },
      "tags": [
        "example tag",
        "another example"
      ]
    }' \
    https://api.linode.com/v4/networking/firewalls
Request Body Schema

devices
object
Devices to create for this Firewall. When a Device is created, the Firewall is assigned to its associated service. Currently, Devices can be created for Linode compute instances and NodeBalancers.

{
  "created": "2018-01-01T00:01:01",
  "id": 123,
  "label": "firewall123",
  "rules": {
    "inbound": [
      {
        "action": "ACCEPT",
        "addresses": {
          "ipv4": [
            "192.0.2.0/24",
            "198.51.100.2/32"
          ],
          "ipv6": [
            "2001:DB8::/128"
          ]
        },
        "description": "An example firewall rule description.",
        "label": "firewallrule123",
        "ports": "22-24, 80, 443",
        "protocol": "TCP"
      }
    ],
    "inbound_policy": "DROP",
    "outbound": [
      {
        "action": "ACCEPT",
        "addresses": {
          "ipv4": [
            "192.0.2.0/24",
            "198.51.100.2/32"
          ],
          "ipv6": [
            "2001:DB8::/128"
          ]
        },
        "description": "An example firewall rule description.",
        "label": "firewallrule123",
        "ports": "22-24, 80, 443",
        "protocol": "TCP"
      }
    ],
    "outbound_policy": "DROP"
  },
  "status": "enabled",
  "tags": [
    "example tag",
    "another example"
  ],
  "updated": "2018-01-02T00:01:01"
}
GET https://api.linode.com/v4/managed/stats
curl -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    https://api.linode.com/v4/managed/stats
AKAMAI ACESSS TOKEN: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72

{
  "data": {
    "cpu": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ],
    "disk": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ],
    "net_in": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ],
    "net_out": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ],
    "swap": [
      {
        "true": 29.94,
        "x": 11513761600000
      }
    ]
  }
}
curl -H "Content-Type: application/json" \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    -X POST \
    https://api.linode.com/v4/managed/services/9994/enable
curl -H "Content-Type: application/json" \
    -H "Authorization: 6692099bd12f686556b7f4e2ae18d783cc500b6432e5a6c5944fb4405c41cd72" \
    -X POST -d '{
      "label": "my-object-storage-key",
      "bucket_access": [
        {
          "cluster": "ap-south-1",
          "bucket_name": "bucket-example-1",
          "permissions": "read_write"
        },
        {
          "cluster": "us-east-1",
          "bucket_name": "bucket-example-2",
          "permissions": "read_only"
        }
      ]
    }' \
  https://api.linode.com/v4/object-storage/keys
{
  "access_key": "KVAKUTGBA4WTR2NSJQ81",
  "bucket_access": [
    {
      "bucket_name": "example-bucket",
      "cluster": "ap-south-1",
      "permissions": "read_only"
    }
  ],
  "id": 123,
  "label": "my-key",
  "limited": true,
  "secret_key": "OiA6F5r0niLs3QA2stbyq7mY5VCV7KqOzcmitmHw"
}    
POST https://api.linode.com/v4/object-storage/keys
About security log events

The name for each audit log entry is composed of a category of events, followed by an operation type. For example, the repo.create entry refers to the create operation on the repo category. The reference information in this article is grouped by categories.
account

Action	Description
account.plan_change	The account's plan changed.
actions_cache

Action	Description
actions_cache.delete	A GitHub Actions cache was deleted using the REST API.
artifact

Action	Description
artifact.destroy	A workflow run artifact was manually deleted.
billing

Action	Description
billing.change_billing_type	The way the account pays for GitHub was changed.
billing.change_email	The billing email address changed.
business

Action	Description
business.set_actions_fork_pr_approvals_policy	The policy for requiring approvals for workflows from public forks was changed for an enterprise.
business.set_actions_private_fork_pr_approvals_policy	The policy for requiring approval for fork pull request workflows from collaborators without write access to private repos was changed for an enterprise.
business.set_actions_retention_limit	The retention period for GitHub Actions artifacts and logs was changed for an enterprise.
business.set_default_workflow_permissions	The default permissions granted to the GITHUB_TOKEN when running workflows were changed for an enterprise.
business.set_fork_pr_workflows_policy	The policy for fork pull request workflows was changed for an enterprise.
business.set_workflow_permission_can_approve_pr	The policy for allowing GitHub Actions to create and approve pull requests was changed for an enterprise.
checks

Action	Description
checks.auto_trigger_disabled	Automatic creation of check suites was disabled on a repository in the organization or enterprise.
checks.auto_trigger_enabled	Automatic creation of check suites was enabled on a repository in the organization or enterprise.
checks.delete_logs	Logs in a check suite were deleted.
codespaces

Action	Description
codespaces.allow_permissions	A codespace using custom permissions from its devcontainer.json file was launched.
codespaces.connect	Credentials for a codespace were refreshed.
codespaces.create	A codespace was created
codespaces.destroy	A user deleted a codespace.
codespaces.export_environment	A codespace was exported to a branch on GitHub.
codespaces.restore	A codespace was restored.
codespaces.start_environment	A codespace was started.
codespaces.suspend_environment	A codespace was stopped.
codespaces.trusted_repositories_access_update	A personal account's access and security setting for Codespaces were updated.
copilot

Action	Description
copilot.cfb_seat_added	A seat was added to the Copilot Business subscription for a user and they have received access to GitHub Copilot.
copilot.cfb_seat_assignment_created	A seat assignment was newly created for a user.
copilot.cfb_seat_assignment_refreshed	A seat assignment that was previously pending cancellation was re-assigned and the user will retain access to GitHub Copilot.
copilot.cfb_seat_assignment_reused	A seat assignment was re-created for a user who already had a seat with no pending cancellation date.
copilot.cfb_seat_assignment_unassigned	A seat was unassigned from a user and they will lose access to GitHub Copilot at the end of the billing cycle.
copilot.cfb_seat_cancelled	A seat was canceled from the Copilot Business subscription and the user no longer has access to GitHub Copilot.
copilot.cfb_seat_cancelled_by_staff	A seat was canceled from the Copilot Business subscription manually by GitHub and the user no longer has access to GitHub Copilot.
dependabot_alerts

Action	Description
dependabot_alerts.disable	Dependabot alerts were disabled for all existing repositories.
dependabot_alerts.enable	Dependabot alerts were enabled for all existing repositories.
dependabot_alerts_new_repos

Action	Description
dependabot_alerts_new_repos.disable	Dependabot alerts were disabled for all new repositories.
dependabot_alerts_new_repos.enable	Dependabot alerts were enabled for all new repositories.
dependabot_repository_access

Action	Description
dependabot_repository_access.repositories_updated	The repositories that Dependabot can access were updated.
dependabot_security_updates

Action	Description
dependabot_security_updates.disable	Dependabot security updates were disabled for all existing repositories.
dependabot_security_updates.enable	Dependabot security updates were enabled for all existing repositories.
dependabot_security_updates_new_repos

Action	Description
dependabot_security_updates_new_repos.disable	Dependabot security updates were disabled for all new repositories.
dependabot_security_updates_new_repos.enable	Dependabot security updates were enabled for all new repositories.
dependency_graph

Action	Description
dependency_graph.disable	The dependency graph was disabled for all existing repositories.
dependency_graph.enable	The dependency graph was enabled for all existing repositories.
dependency_graph_new_repos

Action	Description
dependency_graph_new_repos.disable	The dependency graph was disabled for all new repositories.
dependency_graph_new_repos.enable	The dependency graph was enabled for all new repositories.
environment

Action	Description
environment.add_protection_rule	A GitHub Actions deployment protection rule was created via the API.
environment.create_actions_secret	A secret was created for a GitHub Actions environment.
environment.delete	An environment was deleted.
environment.remove_actions_secret	A secret was deleted for a GitHub Actions environment.
environment.remove_protection_rule	A GitHub Actions deployment protection rule was deleted via the API.
environment.update_actions_secret	A secret was updated for a GitHub Actions environment.
environment.update_protection_rule	A GitHub Actions deployment protection rule was updated via the API.
git_signing_ssh_public_key

Action	Description
git_signing_ssh_public_key.create	An SSH key was added to a user account as a Git commit signing key.
git_signing_ssh_public_key.delete	An SSH key was removed from a user account as a Git commit signing key.
hook

Action	Description
hook.active_changed	A hook's active status was updated.
hook.config_changed	A hook's configuration was changed.
hook.create	A new hook was added.
hook.destroy	A hook was deleted.
hook.events_changed	A hook's configured events were changed.
integration

Action	Description
integration.create	A GitHub App was created.
integration.destroy	A GitHub App was deleted.
integration.manager_added	A member of an enterprise or organization was added as a GitHub App manager.
integration.manager_removed	A member of an enterprise or organization was removed from being a GitHub App manager.
integration.remove_client_secret	A client secret for a GitHub App was removed.
integration.revoke_all_tokens	All user tokens for a GitHub App were requested to be revoked.
integration.revoke_tokens	Token(s) for a GitHub App were revoked.
integration.suspend	A GitHub App was suspended.
integration.transfer	Ownership of a GitHub App was transferred to another user or organization.
integration.unsuspend	A GitHub App was unsuspended.
integration_installation

Action	Description
integration_installation.create	A GitHub App was installed.
integration_installation.destroy	A GitHub App was uninstalled.
integration_installation.repositories_added	Repositories were added to a GitHub App.
integration_installation.repositories_removed	Repositories were removed from a GitHub App.
integration_installation.suspend	A GitHub App was suspended.
integration_installation.unsuspend	A GitHub App was unsuspended.
integration_installation.version_updated	Permissions for a GitHub App were updated.
marketplace_agreement_signature

Action	Description
marketplace_agreement_signature.create	The GitHub Marketplace Developer Agreement was signed.
marketplace_listing

Action	Description
marketplace_listing.approve	A listing was approved for inclusion in GitHub Marketplace.
marketplace_listing.change_category	A category for a listing for an app in GitHub Marketplace was changed.
marketplace_listing.create	A listing for an app in GitHub Marketplace was created.
marketplace_listing.delist	A listing was removed from GitHub Marketplace.
marketplace_listing.redraft	A listing was sent back to draft state.
marketplace_listing.reject	A listing was not accepted for inclusion in GitHub Marketplace.
migration

Action	Description
migration.create	A migration file was created for transferring data from a source location (such as a GitHub.com organization or a GitHub Enterprise Server instance) to a target GitHub Enterprise Server instance.
oauth_access

Action	Description
oauth_access.create	An OAuth access token was generated.
oauth_access.destroy	An OAuth access token was deleted.
oauth_access.regenerate	An OAuth access token was regenerated.
oauth_access.update	An OAuth access token was updated.
oauth_application

Action	Description
oauth_application.create	An OAuth application was created.
oauth_application.destroy	An OAuth application was deleted.
oauth_application.generate_client_secret	An OAuth application's secret key was generated.
oauth_application.remove_client_secret	An OAuth application's secret key was deleted.
oauth_application.reset_secret	The secret key for an OAuth application was reset.
oauth_application.revoke_all_tokens	All user tokens for an OAuth application were requested to be revoked.
oauth_application.revoke_tokens	Token(s) for an OAuth application were revoked.
oauth_application.transfer	An OAuth application was transferred from one account to another.
oauth_authorization

Action	Description
oauth_authorization.create	An authorization for an OAuth application was created.
oauth_authorization.destroy	An authorization for an OAuth application was deleted.
org

Action	Description
org.add_member	A user joined an organization.
org.add_outside_collaborator	An outside collaborator was added to a repository.
org.advanced_security_disabled_for_new_repos	GitHub Advanced Security was disabled for new repositories in an organization.
org.advanced_security_disabled_on_all_repos	GitHub Advanced Security was disabled for all repositories in an organization.
org.advanced_security_enabled_for_new_repos	GitHub Advanced Security was enabled for new repositories in an organization.
org.advanced_security_enabled_on_all_repos	GitHub Advanced Security was enabled for all repositories in an organization.
org.remove_member	A member was removed from an organization, either manually or due to a two-factor authentication requirement.
org.set_actions_fork_pr_approvals_policy	The setting for requiring approvals for workflows from public forks was changed for an organization.
org.set_actions_private_fork_pr_approvals_policy	The policy for requiring approval for fork pull request workflows from collaborators without write access to private repos was changed for an organization.
org.set_actions_retention_limit	The retention period for GitHub Actions artifacts and logs in an organization was changed.
org.set_default_workflow_permissions	The default permissions granted to the GITHUB_TOKEN when running workflows were changed for an organization.
org.set_fork_pr_workflows_policy	The policy for workflows on private repository forks was changed.
org.set_workflow_permission_can_approve_pr	The policy for allowing GitHub Actions to create and approve pull requests was changed for an organization.
org.update_member	A person's role was changed from owner to member or member to owner.
org.update_member_repository_creation_permission	The create repository permission for organization members was changed.
org.update_member_repository_invitation_permission	An organization owner changed the policy setting for organization members inviting outside collaborators to repositories.
pages_protected_domain

Action	Description
pages_protected_domain.create	A GitHub Pages verified domain was created for an organization or enterprise.
pages_protected_domain.delete	A GitHub Pages verified domain was deleted from an organization or enterprise.
pages_protected_domain.verify	A GitHub Pages domain was verified for an organization or enterprise.
passkey

Action	Description
passkey.register	A new passkey was added.
passkey.remove	A new passkey was removed.
payment_method

Action	Description
payment_method.create	A new payment method was added, such as a new credit card or PayPal account.
payment_method.remove	A payment method was removed.
payment_method.update	An existing payment method was updated.
personal_access_token

Action	Description
personal_access_token.access_granted	A fine-grained personal access token was granted access to resources.
personal_access_token.access_revoked	A fine-grained personal access token was revoked. The token can still read public organization resources.
personal_access_token.create	Triggered when you create a fine-grained personal access token.
personal_access_token.credential_regenerated	Triggered when you regenerate a fine-grained personal access token.
personal_access_token.credential_revoked	A fine-grained personal access token was revoked by GitHub Advanced Security.
personal_access_token.destroy	Triggered when you delete a fine-grained personal access token.
personal_access_token.request_cancelled	A pending request for a fine-grained personal access token to access organization resources was canceled.
personal_access_token.request_created	Triggered when a fine-grained personal access token was created to access organization resources and the organization requires approval before the token can access organization resources.
personal_access_token.request_denied	A request for a fine-grained personal access token to access organization resources was denied.
personal_access_token.update	A fine-grained personal access token was updated.
profile_picture

Action	Description
profile_picture.update	A profile picture was updated.
project

Action	Description
project.access	A project board visibility was changed.
project.close	A project board was closed.
project.create	A project board was created.
project.delete	A project board was deleted.
project.link	A repository was linked to a project board.
project.open	A project board was reopened.
project.rename	A project board was renamed.
project.unlink	A repository was unlinked from a project board.
project.update_org_permission	The project's base-level permission for all organization members was changed or removed.
project.update_team_permission	A team's project board permission level was changed or when a team was added or removed from a project board.
project.update_user_permission	A user was added to or removed from a project board or had their permission level changed.
project_field

Action	Description
project_field.create	A field was created in a project board.
project_field.delete	A field was deleted in a project board.
project_view

Action	Description
project_view.create	A view was created in a project board.
project_view.delete	A view was deleted in a project board.
protected_branch

Action	Description
protected_branch.update_merge_queue_enforcement_level	Enforcement of the merge queue was modified for a branch.
public_key

Action	Description
public_key.create	An SSH key was added to a user account or a deploy key was added to a repository.
public_key.delete	An SSH key was removed from a user account or a deploy key was removed from a repository.
public_key.unverification_failure	A user account's SSH key or a repository's deploy key was unable to be unverified.
public_key.unverify	A user account's SSH key or a repository's deploy key was unverified.
public_key.update	A user account's SSH key or a repository's deploy key was updated.
public_key.verification_failure	A user account's SSH key or a repository's deploy key was unable to be verified.
public_key.verify	A user account's SSH key or a repository's deploy key was verified.
repo

Action	Description
repo.access	The visibility of a repository changed.
repo.actions_enabled	GitHub Actions was enabled for a repository.
repo.add_member	A collaborator was added to a repository.
repo.add_topic	A topic was added to a repository.
repo.advanced_security_disabled	GitHub Advanced Security was disabled for a repository.
repo.advanced_security_enabled	GitHub Advanced Security was enabled for a repository.
repo.archived	A repository was archived.
repo.change_merge_setting	Pull request merge options were changed for a repository.
repo.code_scanning_analysis_deleted	Code scanning analysis for a repository was deleted.
repo.code_scanning_configuration_for_branch_deleted	A code scanning configuration for a branch of a repository was deleted.
repo.config.disable_collaborators_only	The interaction limit for collaborators only was disabled.
repo.config.disable_contributors_only	The interaction limit for prior contributors only was disabled in a repository.
repo.config.disable_sockpuppet_disallowed	The interaction limit for existing users only was disabled in a repository.
repo.config.enable_collaborators_only	The interaction limit for collaborators only was enabled in a repository Users that are not collaborators or organization members were unable to interact with a repository for a set duration.
repo.config.enable_contributors_only	The interaction limit for prior contributors only was enabled in a repository Users that are not prior contributors, collaborators or organization members were unable to interact with a repository for a set duration.
repo.config.enable_sockpuppet_disallowed	The interaction limit for existing users was enabled in a repository New users aren't able to interact with a repository for a set duration Existing users of the repository, contributors, collaborators or organization members are able to interact with a repository.
repo.create	A repository was created.
repo.create_actions_secret	A GitHub Actions secret was created for a repository.
repo.create_integration_secret	An integration secret was created for a repository.
repo.destroy	A repository was deleted.
repo.pages_cname	A GitHub Pages custom domain was modified in a repository.
repo.pages_create	A GitHub Pages site was created.
repo.pages_destroy	A GitHub Pages site was deleted.
repo.pages_https_redirect_disabled	HTTPS redirects were disabled for a GitHub Pages site.
repo.pages_https_redirect_enabled	HTTPS redirects were enabled for a GitHub Pages site.
repo.pages_private	A GitHub Pages site visibility was changed to private.
repo.pages_public	A GitHub Pages site visibility was changed to public.
repo.pages_soft_delete	A GitHub Pages site was soft-deleted because its owner's plan changed.
repo.pages_soft_delete_restore	A GitHub Pages site that was previously soft-deleted was restored.
repo.pages_source	A GitHub Pages source was modified.
repo.register_self_hosted_runner	A new self-hosted runner was registered.
repo.remove_actions_secret	A GitHub Actions secret was deleted for a repository.
repo.remove_integration_secret	An integration secret was deleted for a repository.
repo.remove_member	A collaborator was removed from a repository.
repo.remove_self_hosted_runner	A self-hosted runner was removed.
repo.remove_topic	A topic was removed from a repository.
repo.rename	A repository was renamed.
repo.set_actions_fork_pr_approvals_policy	The setting for requiring approvals for workflows from public forks was changed for a repository.
repo.set_actions_private_fork_pr_approvals_policy	The policy for requiring approval for fork pull request workflows from collaborators without write access to private repos was changed for a repository.
repo.set_actions_retention_limit	The retention period for GitHub Actions artifacts and logs in a repository was changed.
repo.set_default_workflow_permissions	The default permissions granted to the GITHUB_TOKEN when running workflows were changed for a repository.
repo.set_fork_pr_workflows_policy	Triggered when the policy for workflows on private repository forks is changed.
repo.set_workflow_permission_can_approve_pr	The policy for allowing GitHub Actions to create and approve pull requests was changed for a repository.
repo.staff_unlock	An enterprise owner or GitHub staff (with permission from a repository administrator) temporarily unlocked the repository.
repo.temporary_access_granted	Temporary access was enabled for a repository.
repo.transfer	A user accepted a request to receive a transferred repository.
repo.transfer_outgoing	A repository was transferred to another repository network.
repo.transfer_start	A user sent a request to transfer a repository to another user or organization.
repo.unarchived	A repository was unarchived.
repo.update_actions_access_settings	The setting to control how a repository was used by GitHub Actions workflows in other repositories was changed.
repo.update_actions_secret	A GitHub Actions secret was updated.
repo.update_actions_settings	A repository administrator changed GitHub Actions policy settings for a repository.
repo.update_default_branch	The default branch for a repository was changed.
repo.update_integration_secret	An integration secret was updated for a repository.
repo.update_member	A user's permission to a repository was changed.
repository_image

Action	Description
repository_image.create	An image to represent a repository was uploaded.
repository_image.destroy	An image to represent a repository was deleted.
repository_invitation

Action	Description
repository_invitation.accept	An invitation to join a repository was accepted.
repository_invitation.cancel	An invitation to join a repository was canceled.
repository_invitation.create	An invitation to join a repository was sent.
repository_invitation.reject	An invitation to join a repository was declined.
repository_ruleset

Action	Description
repository_ruleset.create	A repository ruleset was created.
repository_ruleset.destroy	A repository ruleset was deleted.
repository_ruleset.update	A repository ruleset was edited.
security_key

Action	Description
security_key.register	A security key was registered for an account.
security_key.remove	A security key was removed from an account.
sponsors

Action	Description
sponsors.agreement_sign	A GitHub Sponsors agreement was signed on behalf of an organization.
sponsors.custom_amount_settings_change	Custom amounts for GitHub Sponsors were enabled or disabled, or the suggested custom amount was changed.
sponsors.fiscal_host_change	The fiscal host for a GitHub Sponsors listing was updated.
sponsors.repo_funding_links_file_action	The FUNDING file in a repository was changed.
sponsors.sponsor_sponsorship_cancel	A sponsorship was canceled.
sponsors.sponsor_sponsorship_create	A sponsorship was created, by sponsoring an account.
sponsors.sponsor_sponsorship_payment_complete	After you sponsor an account and a payment has been processed, the sponsorship payment was marked as complete.
sponsors.sponsor_sponsorship_preference_change	The option to receive email updates from a sponsored account was changed.
sponsors.sponsor_sponsorship_tier_change	A sponsorship was upgraded or downgraded.
sponsors.sponsored_developer_approve	A GitHub Sponsors account was approved.
sponsors.sponsored_developer_create	A GitHub Sponsors account was created.
sponsors.sponsored_developer_disable	A GitHub Sponsors account was disabled.
sponsors.sponsored_developer_profile_update	The profile for GitHub Sponsors account was edited.
sponsors.sponsored_developer_redraft	A GitHub Sponsors account was returned to draft state from approved state.
sponsors.sponsored_developer_request_approval	An application for GitHub Sponsors was submitted for approval.
sponsors.sponsored_developer_tier_description_update	The description for a sponsorship tier was changed.
sponsors.sponsored_developer_update_newsletter_send	Triggered when you send an email update to your sponsors.
sponsors.sponsors_patreon_user_create	A Patreon account was linked to a user account for use with GitHub Sponsors.
sponsors.sponsors_patreon_user_destroy	A Patreon account for use with GitHub Sponsors was unlinked from a user account.
sponsors.update_tier_repository	A GitHub Sponsors tier changed access for a repository.
sponsors.update_tier_welcome_message	The welcome message for a GitHub Sponsors tier for an organization was updated.
sponsors.waitlist_join	You join the waitlist to join GitHub Sponsors.
sponsors.withdraw_agreement_signature	A signature was withdrawn from a GitHub Sponsors agreement that applies to an organization.
successor_invitation

Action	Description
successor_invitation.accept	Triggered when you accept a succession invitation.
successor_invitation.cancel	Triggered when you cancel a succession invitation.
successor_invitation.create	Triggered when you create a succession invitation.
successor_invitation.decline	Triggered when you decline a succession invitation.
successor_invitation.revoke	Triggered when you revoke a succession invitation.
trusted_device

Action	Description
trusted_device.register	A new trusted device was added.
trusted_device.remove	A trusted device was removed.
two_factor_authentication

Action	Description
two_factor_authentication.add_factor	A secondary authentication factor was added to a user account.
two_factor_authentication.disabled	Two-factor authentication was disabled for a user account.
two_factor_authentication.enabled	Two-factor authentication was enabled for a user account.
two_factor_authentication.password_reset_fallback_sms	A one-time password code was sent to a user account fallback phone number.
two_factor_authentication.recovery_codes_regenerated	Two factor recovery codes were regenerated for a user account.
two_factor_authentication.remove_factor	A secondary authentication factor was removed from a user account.
two_factor_authentication.sign_in_fallback_sms	A one-time password code was sent to a user account fallback phone number.
two_factor_authentication.update_fallback	The two-factor authentication fallback for a user account was changed.
user

Action	Description
user.add_email	An email address was added to a user account.
user.async_delete	An asynchronous job was started to destroy a user account, eventually triggering a user.delete event.
user.audit_log_export	Audit log entries were exported.
user.block_user	A user was blocked by another user.
user.change_password	A user changed their password.
user.codespaces_trusted_repo_access_granted	Triggered when you allow the codespaces you create for a repository to access other repositories owned by your personal account.
user.codespaces_trusted_repo_access_revoked	Triggered when you disallow the codespaces you create for a repository to access other repositories owned by your personal account.
user.create	A new user account was created.
user.create_integration_secret	A user secret for Codespaces was created.
user.creation_rate_limit_exceeded	The rate of creation of user accounts, applications, issues, pull requests or other resources exceeded the configured rate limits, or too many users were followed too quickly.
user.delete	A user account was destroyed by an asynchronous job.
user.demote	A site administrator was demoted to an ordinary user account.
user.destroy	A user deleted his or her account, triggering user.async_delete.
user.failed_login	A user tried to sign in with an incorrect username, password, or two-factor authentication code.
user.forgot_password	A user requested a password reset.
user.hide_private_contributions_count	A user changed the visibility of their private contributions. The number of contributions to private repositories on the user's profile are now hidden.
user.login	A user signed in.
user.logout	A user signed out.
user.new_device_used	A user signed in from a new device.
user.promote	An ordinary user account was promoted to a site administrator.
user.recreate	A user's account was restored.
user.remove_email	An email address was removed from a user account.
user.remove_integration_secret	A user secret for Codespaces was deleted.
user.rename	A username was changed.
user.reset_password	A user reset their account password.
user.show_private_contributions_count	A user changed the visibility of their private contributions. The number of contributions to private repositories on the user's profile are now shown.
user.sign_in_from_unrecognized_device	A user signed in from an unrecognized device.
user.sign_in_from_unrecognized_device_and_location	A user signed in from an unrecognized device and location.
user.suspend	A user account was suspended.
user.two_factor_challenge_failure	A 2FA challenge issued for a user account failed.
user.two_factor_challenge_success	A 2FA challenge issued for a user account succeeded.
user.two_factor_recover	A user used their 2FA recovery codes.
user.two_factor_recovery_codes_downloaded	A user downloaded 2FA recovery codes for their account.
user.two_factor_recovery_codes_printed	A user printed 2FA recovery codes for their account.
user.two_factor_recovery_codes_viewed	A user viewed 2FA recovery codes for their account.
user.two_factor_requested	A user was prompted for a two-factor authentication code.
user.unblock_user	A user was unblocked by another user.
user.unsuspend	A user account was unsuspended.
user.update_integration_secret	A user secret for Codespaces was updated.
user_status

Action	Description
user_status.destroy	Triggered when you clear the status on your profile.
user_status.update	Triggered when you set or change the status on your profile.
workflows

Action	Description
workflows.approve_workflow_job	A workflow job was approved.
workflows.delete_workflow_run	A workflow run was deleted.
workflows.disable_workflow	A workflow was disabled.
workflows.enable_workflow	A workflow was enabled, after previously being disabled by disable_workflow.
workflows.reject_workflow_job	A workflow job was rejected.

npm smee --url [WEBHOOK_PROXY_UR](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJA)https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJAL --path /webhook --port 3000
Forwarding WEBHOOK_PROXY_URL to http://127.0.0.1:3000/webhook
Connected WEBHOOK_PROXY_URL
gem install bundler
 --global smee-client
bundle init
 bundle install
bundle add sinatra
# These are the dependencies for this code. You installed the `sinatra` gem earlier. For more information, see "[Ruby example: Install dependencies](#ruby-example-install-dependencies)." The `json` library is a standard Ruby library, so you don't need to install it.
require 'sinatra'
require 'json'

# The `/webhook` route matches the path that you specified for the smee.io forwarding. For more information, see "[Forward webhooks](#forward-webhooks)."
#
# Once you deploy your code to a server and update your webhook URL, you should change this to match the path portion of the URL for your webhook.
post '/webhook' do

  # Respond to indicate that the delivery was successfully received.
  # Your server should respond with a 2XX response within 10 seconds of receiving a webhook delivery. If your server takes longer than that to respond, then GitHub terminates the connection and considers the delivery a failure.
  status 202

  # Check the `X-GitHub-Event` header to learn what event type was sent.
  # Sinatra changes `X-GitHub-Event` to `HTTP_X_GITHUB_EVENT`.
  github_event = request.env['[HTTP_X_GITHUB_EVENT](https://scpf-foundation-roblox.fandom.com/wiki/The_Administrator?fbclid=IwAR2FfaoXITYK167Nc-gEZKTMRz_v83X1RrGN52-68b4gcOTDG_Y9pT8S3QY_aem_AcWFgp90kCyN3CxUsNX0uytp_i-7n0Q677zEID8d0e7u0Lh7Ta3Nf6jVo1WXYRibmJAL)']

  # You should add logic to handle each event type that your webhook is subscribed to.
  # For example, this code handles the `issues` and `ping` events.
  #
  # If any events have an `action` field, you should also add logic to handle each action that you are interested in.
  # For example, this code handles the `opened` and `closed` actions for the `issue` event.
  #
  # For more information about the data that you can expect for each event type, see "[AUTOTITLE](/webhooks/webhook-events-and-payloads)."
  if github_event == "issues"
    data = JSON.parse(request.body.read)
    action = data['action']
    if action == "opened"
      puts "An issue was opened with this title: #{data['issue']['title']}"
    elsif action == "closed"
      puts "An issue was closed by #{data['issue']['user']['login']}"
    else
      puts "Unhandled action for the issue event: #{action}"
    end
  elsif github_event == "ping"
    puts "GitHub sent the ping event"
  else
    puts "Unhandled event: #{github_event}"
  end
end

PORT=3000 ruby FILE_NAME
npm install express
// You installed the `express` library earlier. For more information, see "[JavaScript example: Install dependencies](#javascript-example-install-dependencies)."
const express = require('express');

// This initializes a new Express application.
const app = express();

// This defines a POST route at the `/webhook` path. This path matches the path that you specified for the smee.io forwarding. For more information, see "[Forward webhooks](#forward-webhooks)."
//
// Once you deploy your code to a server and update your webhook URL, you should change this to match the path portion of the URL for your webhook.
app.post('/webhook', express.json({type: 'application/json'}), (request, response) => {

  // Respond to indicate that the delivery was successfully received.
  // Your server should respond with a 2XX response within 10 seconds of receiving a webhook delivery. If your server takes longer than that to respond, then GitHub terminates the connection and considers the delivery a failure.
  response.status(202).send('Accepted');

  // Check the `x-github-event` header to learn what event type was sent.
  const githubEvent = request.headers['x-github-event'];

  // You should add logic to handle each event type that your webhook is subscribed to.
  // For example, this code handles the `issues` and `ping` events.
  //
  // If any events have an `action` field, you should also add logic to handle each action that you are interested in.
  // For example, this code handles the `opened` and `closed` actions for the `issue` event.
  //
  // For more information about the data that you can expect for each event type, see "[AUTOTITLE](/webhooks/webhook-events-and-payloads)."
  if (githubEvent === 'issues') {
    const data = request.body;
    const action = data.action;
    if (action === 'opened') {
      console.log(`An issue was opened with this title: ${data.issue.title}`);
    } else if (action === 'closed') {
      console.log(`An issue was closed by ${data.issue.user.login}`);
    } else {
      console.log(`Unhandled action for the issue event: ${action}`);
    }
  } else if (githubEvent === 'ping') {
    console.log('GitHub sent the ping event');
  } else {
    console.log(`Unhandled event: ${githubEvent}`);
  }
});

// This defines the port where your server should listen.
// 3000 matches the port that you specified for webhook forwarding. For more information, see "[Forward webhooks](#forward-webhooks)."
//
// Once you deploy your code to a server, you should change this to match the port where your server is listening.
const port = 3000;

// This starts the server and tells it to listen at the specified port.
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
node THE_ADMINISTRATOR

query {
  viewer {
    repositories(first: 50) {
      edges {
        repository:node {
          name

          issues(first: 10) {
            totalCount
            edges {
              node {
                title
                bodyHTML
              }
            }
          }
        }
      }
    }
  }
}
Calculation:
50         = 50 repositories
 +
50 x 10  = 500 repository issues

            = 550 total nodes
Complex query:
query {
  viewer {
    repositories(first: 50) {
      edges {
        repository:node {
          name

          pullRequests(first: 20) {
            edges {
              pullRequest:node {
                title

                comments(first: 10) {
                  edges {
                    comment:node {
                      bodyHTML
                    }
                  }
                }
              }
            }
          }

          issues(first: 20) {
            totalCount
            edges {
              issue:node {
                title
                bodyHTML

                comments(first: 10) {
                  edges {
                    comment:node {
                      bodyHTML
                    }
                  }
                }
              }
            }
          }
        }
      }
    }

    followers(first: 10) {
      edges {
        follower:node {
          login
        }
      }
    }
  }
}
Calculation:
50              = 50 repositories
 +
50 x 20       = 1,000 pullRequests
 +
50 x 20 x 10 = 10,000 pullRequest comments
 +
50 x 20       = 1,000 issues
 +
50 x 20 x 10 = 10,000 issue comments
 +
10              = 10 followers

                 = 22,060 total nodes
Primary rate limit

The GraphQL API assigns points to each query and limits the points that you can use within a specific amount of time. This limit helps prevent abuse and denial-of-service attacks, and ensures that the API remains available for all users.

The REST API also has a separate primary rate limit. For more information, see "Rate limits for the REST API."

In general, you can calculate your primary rate limit for the GraphQL API based on your method of authentication:

For users: 5,000 points per hour per user. This includes requests made with a personal access token as well as requests made by a GitHub App or OAuth app on behalf of a user that authorized the app. Requests made on a user's behalf by a GitHub App that is owned by a GitHub Enterprise Cloud organization have a higher rate limit of 10,000 points per hour. Similarly, requests made on your behalf by an OAuth app that is owned or approved by a GitHub Enterprise Cloud organization have a higher rate limit of 10,000 points per hour if you are a member of the GitHub Enterprise Cloud organization.
For GitHub App installations not on a GitHub Enterprise Cloud organization: 5,000 points per hour per installation. Installations that have more than 20 repositories receive another 50 points per hour for each repository. Installations that are on an organization that have more than 20 users receive another 50 points per hour for each user. The rate limit cannot increase beyond 12,500 points per hour. The rate limit for user access tokens (as opposed to installation access tokens) are dictated by the primary rate limit for users.
For GitHub App installations on a GitHub Enterprise Cloud organization: 10,000 points per hour per installation. The rate limit for user access tokens (as opposed to installation access tokens) are dictated by the primary rate limit for users.
For OAuth apps: 5,000 points per hour, or 10,000 points per hour if the app is owned by a GitHub Enterprise Cloud organization. This only applies when the app uses their client ID and client secret to request public data. The rate limit for OAuth access tokens generated by a OAuth app are dictated by the primary rate limit for users.
For GITHUB_TOKEN in GitHub Actions workflows: 1,000 points per hour per repository. For requests to resources that belong to an enterprise account on GitHub.com, the limit is 15,000 points per hour per repository.
You can check the point value of a query or calculate the expected point value as described in the following sections. The formula for calculating points and the rate limit are subject to change.

Checking the status of your primary rate limit

You can use the headers that are sent with each response to determine the current status of your primary rate limit.

Header name	Description
x-ratelimit-limit	The maximum number of points that you can use per hour
x-ratelimit-remaining	The number of points remaining in the current rate limit window
x-ratelimit-used	The number of points you have used in the current rate limit window
x-ratelimit-reset	The time at which the current rate limit window resets, in UTC epoch seconds
x-ratelimit-resource	The rate limit resource that the request counted against. For GraphQL requests, this will always be graphql.
You can also query the rateLimit object to check your rate limit. When possible, you should use the rate limit response headers instead of querying the API to check your rate limit.

query {
  viewer {
    login
  }
  rateLimit {
    limit
    remaining
    used
    resetAt
  }
}
Field	Description
limit	The maximum number of points that you can use per hour
remaining	The number of points remaining in the current rate limit window
used	The number of points you have used in the current rate limit window
resetAt	The time at which the current rate limit window resets, in UTC epoch seconds
Returning the point value of a query

You can return the point value of a query by querying the cost field on the rateLimit object:

query {
  viewer {
    login
  }
  rateLimit {
    cost
  }
}
Predicting the point value of a query

You can also roughly calculate the point value of a query before you make the query.

Add up the number of requests needed to fulfill each unique connection in the call. Assume every request will reach the first or last argument limits.
Divide the number by 100 and round the result to the nearest whole number to get the final aggregate point value. This step normalizes large numbers.
Note: The minimum point value of a call to the GraphQL API is 1.
Here's an example query and score calculation:

query {
  viewer {
    login
    repositories(first: 100) {
      edges {
        node {
          id

          issues(first: 50) {
            edges {
              node {
                id

                labels(first: 60) {
                  edges {
                    node {
                      id
                      name
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}

 
