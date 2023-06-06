mkdir helm-course
cd helm-course
helm create first-chart # generates boilerplate helmchart template
ls first-chart/

# Install a chart
helm install first-chart .
# Check templates
helm template first-chart .
# Upgrade chart
helm upgrade first-chart .
# Check histry 
helm history first-chart
# Rollback
helm rollback first-chart 
helm rollback first-chart <REVISION_NUMBER>
# base64 encoding
echo -n 'admin' | base64

# Get a list of Helm charts
helm list
# delete chart
helm delete <release-name> --dry-run