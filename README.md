# ObjectFlow.Core.Extensibility

Objectflow provides developers with a straight-forward way of separating business logic from control flow. This leads to more flexible software that is cheaper to change. With this library you can use it via JSON definition files.

```json

[
    {
        "Name": "StepOne",
        "DisplayName": "Step One Description",
        "Priority": 0,
        "DependsOn": [],
        "Handler": "My.Cool.Steps.Library.StepOne, My.Cool.Steps.Library"
    },
    {
        "Name": "StepTwo",
        "DisplayName": "Step Two Description",
        "Priority": 0,
        "DependsOn": [],
        "Handler": "My.Cool.Steps.Library.StepTwo, My.Cool.Steps.Library"
    },    
    {
        "Name": "StepThree",
        "DisplayName": "Step Three Description",
        "Priority": 0,
        "DependsOn": [ "StepOne", "StepTwo" ],
        "Handler": "My.Cool.Steps.Library.StepThree, My.Cool.Steps.Library"
    },
    {
        "Name": "StepFour",
        "DisplayName": "Step Four Description",
        "Priority": 0,
        "DependsOn": [ "StepThree" ],
        "Handler": "My.Cool.Steps.Library.StepThree, My.Cool.Steps.Library",
        "Scope": "My.Cool.Scope.Library.AnotherScope, My.Cool.Scope.Library"
    }
]

```

```csharp

public class AnotherScope : IOperationScope<IssueCommand>
    {
        public string Name
        {
            get { return "AnotherScope"; }
        }

        public IssueCommand Execute(IOperation<IssueCommand> operation, IssueCommand data)
        {
            Task.Run(() =>
            {
                operation.Execute(data);
            });            
        }
    }
    
```
