# The order to execute of this example
    kubectl create -f app-deployment.yaml -f app-service.yaml --kubeconfig=config
    kubectl create namespace ingress --kubeconfig=config
    kubectl create -f app-default-backend-deployment.yaml -f app-default-backend-service.yaml -n=ingress --kubeconfig=admin.conf
    kubectl create -f app-nginx-ingress-controller-config-map.yaml -n=ingress --kubeconfig=admin.conf
    kubectl create -f app-nginx-ingress-controller-roles.yaml -n=ingress --kubeconfig=admin.conf
    kubectl create -f app-nginx-ingress-controller-deployment.yaml -n=ingress --kubeconfig=admin.conf

    kubectl create -f app-nginx-ingress.yaml -n=ingress --kubeconfig=admin.conf
    kubectl create -f app-ingress.yaml --kubeconfig=admin.conf
    kubectl create -f app-nginx-ingress-controller-service.yaml -n=ingress --kubeconfig=admin.conf

## No dns? Then, do it on your laptop
    echo "${LOCALHOST_IP} tedsite01.com" | sudo tee -a /etc/hosts

    You can verify everything works fine by accessing to those endpoints:

    http://tedsite01.com:30000/app1
    http://tedsite01.com:30000/app2
    http://tedsite01.com:30000/nginx_status

## Comment
    Any other endpoint will redirect the request to default backend. 
    Ingress controller is fully functional now and you could add more apps to it. 
    For any problems during the setup please leave a comment. 