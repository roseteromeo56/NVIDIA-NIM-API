![nvidia-logo](https://github.com/user-attachments/assets/3720336a-731b-4284-9862-3de8543adbc5)
# NVIDIA-NIM-API
Owner    nvcr.io/nim/meta/llama3-70b-instruct:1.0.3  
Associated Products
NVIDIA Developer Program
NVIDIA AI Enterprise Essentials
Features
NVIDIA NIM
NVIDIA AI Enterprise Supported
Description
NVIDIA NIM for GPU accelerated Llama 3 70B inference through OpenAI compatible APIs
Publisher
NVIDIA
Latest Tag
1.0.3
Modified
April 11, 2025
Compressed Size
5.98 GB
Multinode Support
No
Multi-Arch Support
No
1.0.3 (Latest) Security Scan Results
Linux / amd64

C
signed images
Automotive / Transportation
Llama3-70b-instruct
NSPECT-MB5F-LVUL
NVIDIA AI Enterprise Supported
NVIDIA NIM
llama3
helm fetch https://helm.ngc.nvidia.com/nvidia/charts/gpu-operator-v25.3.0.tgz
GitHub license
![image](https://github.com/user-attachments/assets/1936f07c-0cbc-4b1a-b531-438245bf8df9)
https://integrate.api.nvidia.com/v1/chat/completions
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
---
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  annotations:
    controller-gen.kubebuilder.io/version: v0.16.3
  name: nodefeatures.nfd.k8s-sigs.io
spec:
  group: nfd.k8s-sigs.io
  names:
    kind: NodeFeature
    listKind: NodeFeatureList
    plural: nodefeatures
    singular: nodefeature
  scope: Namespaced
  versions:
  - name: v1alpha1
    schema:
      openAPIV3Schema:
        description: |-
          NodeFeature resource holds the features discovered for one node in the
          cluster.
        properties:
          apiVersion:
            description: |-
              APIVersion defines the versioned schema of this representation of an object.
              Servers should convert recognized schemas to the latest internal value, and
              may reject unrecognized values.
              More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources
            type: string
          kind:
            description: |-
              Kind is a string value representing the REST resource this object represents.
              Servers may infer this from the endpoint the client submits requests to.
              Cannot be updated.
              In CamelCase.
              More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds
            type: string
          metadata:
            type: object
          spec:
            description: Specification of the NodeFeature, containing features discovered
              for a node.
            properties:
              features:
                description: Features is the full "raw" features data that has been
                  discovered.
                properties:
                  attributes:
                    additionalProperties:
                      description: AttributeFeatureSet is a set of features having
                        string value.
                      properties:
                        elements:
                          additionalProperties:
                            type: string
                          description: Individual features of the feature set.
                          type: object
                      required:
                      - elements
                      type: object
                    description: Attributes contains all the attribute-type features
                      of the node.
                    type: object
                  flags:
                    additionalProperties:
                      description: FlagFeatureSet is a set of simple features only
                        containing names without values.
                      properties:
                        elements:
                          additionalProperties:
                            description: |-
                              Nil is a dummy empty struct for protobuf compatibility.
                              NOTE: protobuf definitions have been removed but this is kept for API compatibility.
                            type: object
                          description: Individual features of the feature set.
                          type: object
                      required:
                      - elements
                      type: object
                    description: Flags contains all the flag-type features of the
                      node.
                    type: object
                  instances:
                    additionalProperties:
                      description: InstanceFeatureSet is a set of features each of
                        which is an instance having multiple attributes.
                      properties:
                        elements:
                          description: Individual features of the feature set.
                          items:
                            description: InstanceFeature represents one instance of
                              a complex features, e.g. a device.
                            properties:
                              attributes:
                                additionalProperties:
                                  type: string
                                description: Attributes of the instance feature.
                                type: object
                            required:
                            - attributes
                            type: object
                          type: array
                      required:
                      - elements
                      type: object
                    description: Instances contains all the instance-type features
                      of the node.
                    type: object
                type: object
              labels:
                additionalProperties:
                  type: string
                description: Labels is the set of node labels that are requested to
                  be created.
                type: object
            type: object
        required:
        - spec
        type: object
    served: true
    storage: true
---
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  annotations:
    controller-gen.kubebuilder.io/version: v0.16.3
  name: nodefeaturegroups.nfd.k8s-sigs.io
spec:
  group: nfd.k8s-sigs.io
  names:
    kind: NodeFeatureGroup
    listKind: NodeFeatureGroupList
    plural: nodefeaturegroups
    shortNames:
    - nfg
    singular: nodefeaturegroup
  scope: Namespaced
  versions:
  - name: v1alpha1
    schema:
      openAPIV3Schema:
        description: NodeFeatureGroup resource holds Node pools by featureGroup
        properties:
          apiVersion:
            description: |-
              APIVersion defines the versioned schema of this representation of an object.
              Servers should convert recognized schemas to the latest internal value, and
              may reject unrecognized values.
              More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources
            type: string
          kind:
            description: |-
              Kind is a string value representing the REST resource this object represents.
              Servers may infer this from the endpoint the client submits requests to.
              Cannot be updated.
              In CamelCase.
              More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds
            type: string
          metadata:
            type: object
          spec:
            description: Spec defines the rules to be evaluated.
            properties:
              featureGroupRules:
                description: List of rules to evaluate to determine nodes that belong
                  in this group.
                items:
                  description: GroupRule defines a rule for nodegroup filtering.
                  properties:
                    matchAny:
                      description: MatchAny specifies a list of matchers one of which
                        must match.
                      items:
                        description: MatchAnyElem specifies one sub-matcher of MatchAny.
                        properties:
                          matchFeatures:
                            description: MatchFeatures specifies a set of matcher
                              terms all of which must match.
                            items:
                              description: |-
                                FeatureMatcherTerm defines requirements against one feature set. All
                                requirements (specified as MatchExpressions) are evaluated against each
                                element in the feature set.
                              properties:
                                feature:
                                  description: Feature is the name of the feature
                                    set to match against.
                                  type: string
                                matchExpressions:
                                  additionalProperties:
                                    description: |-
                                      MatchExpression specifies an expression to evaluate against a set of input
                                      values. It contains an operator that is applied when matching the input and
                                      an array of values that the operator evaluates the input against.
                                    properties:
                                      op:
                                        description: Op is the operator to be applied.
                                        enum:
                                        - In
                                        - NotIn
                                        - InRegexp
                                        - Exists
                                        - DoesNotExist
                                        - Gt
                                        - Lt
                                        - GtLt
                                        - IsTrue
                                        - IsFalse
                                        type: string
                                      value:
                                        description: |-
                                          Value is the list of values that the operand evaluates the input
                                          against. Value should be empty if the operator is Exists, DoesNotExist,
                                          IsTrue or IsFalse. Value should contain exactly one element if the
                                          operator is Gt or Lt and exactly two elements if the operator is GtLt.
                                          In other cases Value should contain at least one element.
                                        items:
                                          type: string
                                        type: array
                                    required:
                                    - op
                                    type: object
                                  description: |-
                                    MatchExpressions is the set of per-element expressions evaluated. These
                                    match against the value of the specified elements.
                                  type: object
                                matchName:
                                  description: |-
                                    MatchName in an expression that is matched against the name of each
                                    element in the feature set.
                                  properties:
                                    op:
                                      description: Op is the operator to be applied.
                                      enum:
                                      - In
                                      - NotIn
                                      - InRegexp
                                      - Exists
                                      - DoesNotExist
                                      - Gt
                                      - Lt
                                      - GtLt
                                      - IsTrue
                                      - IsFalse
                                      type: string
                                    value:
                                      description: |-
                                        Value is the list of values that the operand evaluates the input
                                        against. Value should be empty if the operator is Exists, DoesNotExist,
                                        IsTrue or IsFalse. Value should contain exactly one element if the
                                        operator is Gt or Lt and exactly two elements if the operator is GtLt.
                                        In other cases Value should contain at least one element.
                                      items:
                                        type: string
                                      type: array
                                  required:
                                  - op
                                  type: object
                              required:
                              - feature
                              type: object
                            type: array
                        required:
                        - matchFeatures
                        type: object
                      type: array
                    matchFeatures:
                      description: MatchFeatures specifies a set of matcher terms
                        all of which must match.
                      items:
                        description: |-
                          FeatureMatcherTerm defines requirements against one feature set. All
                          requirements (specified as MatchExpressions) are evaluated against each
                          element in the feature set.
                        properties:
                          feature:
                            description: Feature is the name of the feature set to
                              match against.
                            type: string
                          matchExpressions:
                            additionalProperties:
                              description: |-
                                MatchExpression specifies an expression to evaluate against a set of input
                                values. It contains an operator that is applied when matching the input and
                                an array of values that the operator evaluates the input against.
                              properties:
                                op:
                                  description: Op is the operator to be applied.
                                  enum:
                                  - In
                                  - NotIn
                                  - InRegexp
                                  - Exists
                                  - DoesNotExist
                                  - Gt
                                  - Lt
                                  - GtLt
                                  - IsTrue
                                  - IsFalse
                                  type: string
                                value:
                                  description: |-
                                    Value is the list of values that the operand evaluates the input
                                    against. Value should be empty if the operator is Exists, DoesNotExist,
                                    IsTrue or IsFalse. Value should contain exactly one element if the
                                    operator is Gt or Lt and exactly two elements if the operator is GtLt.
                                    In other cases Value should contain at least one element.
                                  items:
                                    type: string
                                  type: array
                              required:
                              - op
                              type: object
                            description: |-
                              MatchExpressions is the set of per-element expressions evaluated. These
                              match against the value of the specified elements.
                            type: object
                          matchName:
                            description: |-
                              MatchName in an expression that is matched against the name of each
                              element in the feature set.
                            properties:
                              op:
                                description: Op is the operator to be applied.
                                enum:
                                - In
                                - NotIn
                                - InRegexp
                                - Exists
                                - DoesNotExist
                                - Gt
                                - Lt
                                - GtLt
                                - IsTrue
                                - IsFalse
                                type: string
                              value:
                                description: |-
                                  Value is the list of values that the operand evaluates the input
                                  against. Value should be empty if the operator is Exists, DoesNotExist,
                                  IsTrue or IsFalse. Value should contain exactly one element if the
                                  operator is Gt or Lt and exactly two elements if the operator is GtLt.
                                  In other cases Value should contain at least one element.
                                items:
                                  type: string
                                type: array
                            required:
                            - op
                            type: object
                        required:
                        - feature
                        type: object
                      type: array
                    name:
                      description: Name of the rule.
                      type: string
                  required:
                  - name
                  type: object
                type: array
            required:
            - featureGroupRules
            type: object
          status:
            description: |-
              Status of the NodeFeatureGroup after the most recent evaluation of the
              specification.
            properties:
              nodes:
                description: Nodes is a list of FeatureGroupNode in the cluster that
                  match the featureGroupRules
                items:
                  properties:
                    name:
                      description: Name of the node.
                      type: string
                  required:
                  - name
                  type: object
                type: array
                x-kubernetes-list-map-keys:
                - name
                x-kubernetes-list-type: map
            type: object
        required:
        - spec
        type: object
    served: true
    storage: true
    subresources:
      status: {}
---
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  annotations:
    controller-gen.kubebuilder.io/version: v0.16.3
  name: nodefeaturerules.nfd.k8s-sigs.io
spec:
  group: nfd.k8s-sigs.io
  names:
    kind: NodeFeatureRule
    listKind: NodeFeatureRuleList
    plural: nodefeaturerules
    shortNames:
    - nfr
    singular: nodefeaturerule
  scope: Cluster
  versions:
  - name: v1alpha1
    schema:
      openAPIV3Schema:
        description: |-
          NodeFeatureRule resource specifies a configuration for feature-based
          customization of node objects, such as node labeling.
        properties:
          apiVersion:
            description: |-
              APIVersion defines the versioned schema of this representation of an object.
              Servers should convert recognized schemas to the latest internal value, and
              may reject unrecognized values.
              More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources
            type: string
          kind:
            description: |-
              Kind is a string value representing the REST resource this object represents.
              Servers may infer this from the endpoint the client submits requests to.
              Cannot be updated.
              In CamelCase.
              More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds
            type: string
          metadata:
            type: object
          spec:
            description: Spec defines the rules to be evaluated.
            properties:
              rules:
                description: Rules is a list of node customization rules.
                items:
                  description: Rule defines a rule for node customization such as
                    labeling.
                  properties:
                    annotations:
                      additionalProperties:
                        type: string
                      description: Annotations to create if the rule matches.
                      type: object
                    extendedResources:
                      additionalProperties:
                        type: string
                      description: ExtendedResources to create if the rule matches.
                      type: object
                    labels:
                      additionalProperties:
                        type: string
                      description: Labels to create if the rule matches.
                      type: object
                    labelsTemplate:
                      description: |-
                        LabelsTemplate specifies a template to expand for dynamically generating
                        multiple labels. Data (after template expansion) must be keys with an
                        optional value (<key>[=<value>]) separated by newlines.
                      type: string
                    matchAny:
                      description: MatchAny specifies a list of matchers one of which
                        must match.
                      items:
                        description: MatchAnyElem specifies one sub-matcher of MatchAny.
                        properties:
                          matchFeatures:
                            description: MatchFeatures specifies a set of matcher
                              terms all of which must match.
                            items:
                              description: |-
                                FeatureMatcherTerm defines requirements against one feature set. All
                                requirements (specified as MatchExpressions) are evaluated against each
                                element in the feature set.
                              properties:
                                feature:
                                  description: Feature is the name of the feature
                                    set to match against.
                                  type: string
                                matchExpressions:
                                  additionalProperties:
                                    description: |-
                                      MatchExpression specifies an expression to evaluate against a set of input
                                      values. It contains an operator that is applied when matching the input and
                                      an array of values that the operator evaluates the input against.
                                    properties:
                                      op:
                                        description: Op is the operator to be applied.
                                        enum:
                                        - In
                                        - NotIn
                                        - InRegexp
                                        - Exists
                                        - DoesNotExist
                                        - Gt
                                        - Lt
                                        - GtLt
                                        - IsTrue
                                        - IsFalse
                                        type: string
                                      value:
                                        description: |-
                                          Value is the list of values that the operand evaluates the input
                                          against. Value should be empty if the operator is Exists, DoesNotExist,
                                          IsTrue or IsFalse. Value should contain exactly one element if the
                                          operator is Gt or Lt and exactly two elements if the operator is GtLt.
                                          In other cases Value should contain at least one element.
                                        items:
                                          type: string
                                        type: array
                                    required:
                                    - op
                                    type: object
                                  description: |-
                                    MatchExpressions is the set of per-element expressions evaluated. These
                                    match against the value of the specified elements.
                                  type: object
                                matchName:
                                  description: |-
                                    MatchName in an expression that is matched against the name of each
                                    element in the feature set.
                                  properties:
                                    op:
                                      description: Op is the operator to be applied.
                                      enum:
                                      - In
                                      - NotIn
                                      - InRegexp
                                      - Exists
                                      - DoesNotExist
                                      - Gt
                                      - Lt
                                      - GtLt
                                      - IsTrue
                                      - IsFalse
                                      type: string
                                    value:
                                      description: |-
                                        Value is the list of values that the operand evaluates the input
                                        against. Value should be empty if the operator is Exists, DoesNotExist,
                                        IsTrue or IsFalse. Value should contain exactly one element if the
                                        operator is Gt or Lt and exactly two elements if the operator is GtLt.
                                        In other cases Value should contain at least one element.
                                      items:
                                        type: string
                                      type: array
                                  required:
                                  - op
                                  type: object
                              required:
                              - feature
                              type: object
                            type: array
                        required:
                        - matchFeatures
                        type: object
                      type: array
                    matchFeatures:
                      description: MatchFeatures specifies a set of matcher terms
                        all of which must match.
                      items:
                        description: |-
                          FeatureMatcherTerm defines requirements against one feature set. All
                          requirements (specified as MatchExpressions) are evaluated against each
                          element in the feature set.
                        properties:
                          feature:
                            description: Feature is the name of the feature set to
                              match against.
                            type: string
                          matchExpressions:
                            additionalProperties:
                              description: |-
                                MatchExpression specifies an expression to evaluate against a set of input
                                values. It contains an operator that is applied when matching the input and
                                an array of values that the operator evaluates the input against.
                              properties:
                                op:
                                  description: Op is the operator to be applied.
                                  enum:
                                  - In
                                  - NotIn
                                  - InRegexp
                                  - Exists
                                  - DoesNotExist
                                  - Gt
                                  - Lt
                                  - GtLt
                                  - IsTrue
                                  - IsFalse
                                  type: string
                                value:
                                  description: |-
                                    Value is the list of values that the operand evaluates the input
                                    against. Value should be empty if the operator is Exists, DoesNotExist,
                                    IsTrue or IsFalse. Value should contain exactly one element if the
                                    operator is Gt or Lt and exactly two elements if the operator is GtLt.
                                    In other cases Value should contain at least one element.
                                  items:
                                    type: string
                                  type: array
                              required:
                              - op
                              type: object
                            description: |-
                              MatchExpressions is the set of per-element expressions evaluated. These
                              match against the value of the specified elements.
                            type: object
                          matchName:
                            description: |-
                              MatchName in an expression that is matched against the name of each
                              element in the feature set.
                            properties:
                              op:
                                description: Op is the operator to be applied.
                                enum:
                                - In
                                - NotIn
                                - InRegexp
                                - Exists
                                - DoesNotExist
                                - Gt
                                - Lt
                                - GtLt
                                - IsTrue
                                - IsFalse
                                type: string
                              value:
                                description: |-
                                  Value is the list of values that the operand evaluates the input
                                  against. Value should be empty if the operator is Exists, DoesNotExist,
                                  IsTrue or IsFalse. Value should contain exactly one element if the
                                  operator is Gt or Lt and exactly two elements if the operator is GtLt.
                                  In other cases Value should contain at least one element.
                                items:
                                  type: string
                                type: array
                            required:
                            - op
                            type: object
                        required:
                        - feature
                        type: object
                      type: array
                    name:
                      description: Name of the rule.
                      type: string
                    taints:
                      description: Taints to create if the rule matches.
                      items:
                        description: |-
                          The node this Taint is attached to has the "effect" on
                          any pod that does not tolerate the Taint.
                        properties:
                          effect:
                            description: |-
                              Required. The effect of the taint on pods
                              that do not tolerate the taint.
                              Valid effects are NoSchedule, PreferNoSchedule and NoExecute.
                            type: string
                          key:
                            description: Required. The taint key to be applied to
                              a node.
                            type: string
                          timeAdded:
                            description: |-
                              TimeAdded represents the time at which the taint was added.
                              It is only written for NoExecute taints.
                            format: date-time
                            type: string
                          value:
                            description: The taint value corresponding to the taint
                              key.
                            type: string
                        required:
                        - effect
                        - key
                        type: object
                      type: array
                    vars:
                      additionalProperties:
                        type: string
                      description: |-
                        Vars is the variables to store if the rule matches. Variables do not
                        directly inflict any changes in the node object. However, they can be
                        referenced from other rules enabling more complex rule hierarchies,
                        without exposing intermediary output values as labels.
                      type: object
                    varsTemplate:
                      description: |-
                        VarsTemplate specifies a template to expand for dynamically generating
                        multiple variables. Data (after template expansion) must be keys with an
                        optional value (<key>[=<value>]) separated by newlines.
                      type: string
                  required:
                  - name
                  type: object
                type: array
            required:
            - rules
            type: object
        required:
        - spec
        type: object
    served: true
    storage: true
Secure coding/Trial GitHub Advanced Security/
Exploring your enterprise trial of GitHub Code Security
Introduction to the features of code and dependency scanning available with GitHub Code Security in GitHub Enterprise Cloud so you can assess their fit to your business needs.

In this article
Introduction
Evaluate and refine results from the default setup
Enforce automated analysis of pull requests
Define where Copilot Autofix is allowed and enabled
Engage developers in security remediation
Provide a secure development environment
Next steps
Further reading
This guide assumes that you have planned and started a trial of GitHub Advanced Security for an existing or trial GitHub enterprise account, see Planning a trial of GitHub Advanced Security.

Introduction
Code scanning and dependency analysis work in the same way in public repositories and in private and internal repositories with Code Security enabled. In addition, Code Security enables you to create security campaigns where security specialists and developers can collaborate to effectively reduce technical debt.

This article focuses on how you can combine these features with enterprise-level controls to standardize and enforce your development process.

Refine your security configurations
In contrast to Secret Protection, where a single security configuration is typically applied to all repositories, you probably want to fine-tune the configuration of code scanning for different types of repositories. For example, you might need to create additional configurations so that:

Code scanning uses runners with a specific label to apply to repositories that require a specialized environment or that use private registeries.
Code scanning is "Not set" to apply to repositories that need to use advanced setup or that require a third-party tool.
For your trial, it's simplest to create a primary enterprise-level security configuration and apply it to your test repositories. Then you can create any additional security configurations you need and apply them to a subset of repositories selected using code language, custom property, visibility, and other filter options. For more information, see Enabling security features in your trial enterprise and Applying a custom security configuration.

Provide access to view results of code scanning
By default, only the repository administrator and the organization owner can view all code scanning alerts in their area. You should assign the predefined security manager role to all organization teams and users who you want to access the alerts found during the trial. You may also want to give the enterprise account owner this role for each organization in the trial. For more information, see Managing security managers in your organization and Using organization roles.

Evaluate and refine results from the default setup
The default setup for code scanning runs a set of high confidence queries. These are chosen to ensure that, when you roll out code scanning across your whole codebase, developers see a limited set of high quality results, with few false positive results.

You can see a summary of any results found in the organizations in your trial enterprise in the  Security tab for the enterprise. There are also separate views for each type of security alert. See Viewing security insights.

If you don't see the results you expect for code scanning, you can update default setup to run an extended query suite for repositories where you expected to find more results. This is controlled at the repository level, see Editing your configuration of default setup.

Tip

If you are blocked from editing the repository settings for code scanning, edit the security configuration used by the repository so that settings are not enforced.

If the extended suite still fails to find the results you expect, you may need to enable advanced setup so you can customize the analysis fully. For more information, see About the tool status page for code scanning and Configuring advanced setup for code scanning.

Enforce automated analysis of pull requests
There are three different types of automated analysis of pull requests built into GitHub:

Code scanning analysis uses queries to highlight known bad coding patterns and security vulnerabilities. Copilot Autofix suggests fixes to problems identified by code scanning.
Dependency review summarizes the dependency changes made by the pull request and highlights any dependencies with known vulnerabilities or that do not meet your development standards.
Copilot code review uses AI to provide feedback on your changes with suggested fixes where possible.
These automated reviews are a valuable extension to self-review and make it easier for developers to present a more complete and secure pull request for peer review. In addition, code scanning and dependency reviews can be enforced to protect the security and compliance of your code.

Note

GitHub Copilot Autofix is included in the license for GitHub Code Security. Copilot code review requires a paid Copilot plan.

Code scanning analysis
When code scanning is enabled, you can then block merges into important branches unless the pull request meets your requirements by creating a code ruleset for the enterprise or organization. Typically, you would require that results from code scanning are present and that any important alerts are resolved.

Type of ruleset: Branch.
Require code scanning results: Enable to block merging until results are successfully generated for the commit and the reference the pull request targets.
Required tools and alert thresholds: Define the level of alerts that must be resolved before a pull request can be merged for each code scanning tool you use.
As with all rulesets, you can control exactly which organizations (enterprise-level), repositories, and branches it acts on and also define roles or teams who can bypass the rule. For more information, see About rulesets.

Dependency review
When Code Security and dependency graph are enabled for a repository, manifest files have a rich diff view which shows a summary of the dependencies that it adds or updates. This is a useful summary for human reviewers of the pull request but does not provide any control of which dependencies are added to the codebase.

Most enterprises put automatic checks in place to block the use of dependencies with known vulnerabilities or unsupported license terms.

Create a private repository to serve as a central home where you can store reusable workflows for the enterprise.
Edit the actions settings for the repository to allow all private repositories in the enterprise to access workflows in this central repository, see Allowing access to components in a private repository.
In the central repository, create a reusable workflow to run the dependency review action, configuring the action to meet your business needs, see Configuring the dependency review action.
In each organization, create or update branch rulesets to add the new workflow to the required status checks, see Enforcing dependency review across an organization.
This allows you to update the configuration in a single location, but use the workflow in many repositories. You may want to use this central repository to maintain other workflows. For more information, see Reusing workflows.

Copilot review
Note

GitHub Copilot code review is in public preview and subject to change.
The GitHub Pre-release License Terms apply to your use of this product.
If you get a Copilot subscription from an organization, you will only be able to participate in the public preview on the GitHub website if an owner of your organization has enabled Copilot in GitHub.com > Opt in to preview features in the GitHub Copilot policies page of the organization settings. See Managing policies for Copilot in your organization.
By default, users request a review from Copilot in the same way as they do from human reviewers. However, you can update or create an organization-level branch ruleset to automatically add Copilot as a reviewer to all pull requests made to selected branches in all or selected repositories. See Configuring automatic code review by Copilot.

Copilot leaves a review comment on each pull request it reviews, without approving the pull request or requesting changes. This ensures that its review is advisory and will not block development work. Similarly, you should not enforce the resolution of suggestions made by Copilot because AI suggestions have known limitations, see Responsible use of GitHub Copilot code review.

Define where Copilot Autofix is allowed and enabled
Copilot Autofix helps developers understand and fix code scanning alerts found in their pull requests. We recommend that you enable this feature for all repositories with Code Security enabled to help developers resolve alerts efficiently and increase their understanding of secure coding.

There are two levels of control:

Enterprises can allow or block use of Copilot Autofix throughout the enterprise using an "Advanced Security" policy, see: Enforcing policies for code security and analysis for your enterprise.
Organizations can enable or disable Copilot Autofix for all organization-owned repositories in the "Global settings" for the organization, see Configuring global security settings for your organization.
Engage developers in security remediation
Security campaigns provide a way for security teams to engage with developers to remediate security technical debt. They also provide a practical way to combine education in secure coding with examples of vulnerable code in code that your developers are familar with. For more information, see About security campaigns and Best practices for fixing security alerts at scale.

Provide a secure development environment
The development environment has many components. Some of the most useful features for scaling and standardizing a secure development environment in GitHub are:

Security configurations: define the setup of security features for the enterprise, an organization, a subset of organization repositories, or new repositories, see Refine your security configurations.
Policies: protect and control use of resources for the enterprise or an organization, see Enforcing policies for your enterprise.
Rulesets: protect and control branches, tags, and pushes for an organization, a subset of organization repositories, or a repository, see Creating rulesets for repositories in your organization.
Repository templates: define the security workflows and processes needed for each type of environment, see Creating a template repository. For example, each template might contain a specialized:
Security policy file defining the company's security stance and how to report any security concerns.
Workflow to enable Dependabot version updates for package managers used by the company.
Workflow defining advanced setup for code scanning for supported development languages where the default setup results are not enough.
In addition, when a developer creates a repository from a template they must define the value of any required custom properties. Custom properties are very useful for selecting a subset of repositories that you want to apply configurations, policies, or rulesets to, see Managing custom properties for repositories in your enterprise.

Next steps
When you have finished exploring these options and secret scanning features, you are ready to test your discoveries so far against your business needs, and then explore further.

Further reading
Security hardening for GitHub Actions
Enforcing policies for your enterprise
Governing how people use repositories in your enterprise
Enforce GitHub Advanced Security at Scale
Help and support
Did you find what you needed?

Privacy policy
Help us make these docs great!
All GitHub docs are open source. See something that's wrong or unclear? Submit a pull request.

Learn how to contribute

Still need help?
Ask the GitHub community
Contact support
Legal
© 2025 GitHub, Inc.
Terms
Privacy
Status
Pricing
Expert services
Blog
