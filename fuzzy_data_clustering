x = [2.5 3.0 3.0 3.5 5.5 6.0 6.0 6.5 4.5 10 10;
    3.5 3.0 4.0 3.5 5.5 6.0 5.0 5.5 4.5 10 10];
pN = size(x);
c = 3; %Amount of groups
eps = 10^-5;
m = 2; %Fuzziness
t = 0; %Iteration counter
u = zeros(c,pN(2)); %Partition matrix

check = 1;

for i=1:pN(2)
    r = rand(1, c); % Start with c random numbers that don't sum to 1.
    r = r / sum(r);  % Normalize so the sum is 1.
    
    r = r.';    % transpose -> becomes vertical
    
    u(:,i) = r;
end
% generating val equal to 1 vertically



for i=1:c %Check if any row isn't empty, if yes terminate the code
    if sum(u(i,:))==0
        print("Incorrectly generated initial partition matrix - Please try again.")
        exit
    end
end

u;
while check>eps
    t = t+1
    v = zeros(pN(1),c);
    for i=1:pN(1)
        for j=1:c
            uTemp = u.^m;
            tempV = uTemp(j,:).*x(i,:)
            v(i,j) = sum(tempV)/sum(uTemp(j,:));
        end
    end
    v;
%     for i = 1:c
%         for j = 1:pN(1)
%             Nominator = 0;
%             Denominator = 0;
%             for k = 1:pN(2)
%                 Nominator = Nominator + u(i, k) ^ m * x(j, k);
%                 Denominator = Denominator + u(i, k) ^ m;
%             end
%             if Denominator ~= 0
%                 v(j, i) = Nominator / Denominator;
%             end
%         end
%     end


    d = zeros(c,pN(2))
    for i=1:pN(2)
        for j=1:c
          d(j,i) = sqrt((x(1,i)-v(1,j))^2+(x(2,i)-v(2,j))^2);
        end
    end
d
    temp = uTemp.*(d.^2);
    tempSum = sum(temp);
    jVal = sum(tempSum);

    uOld = u;
    dForNewU = d.^(2/(1-m));
    for i=1:c
        for j=1:pN(2)
            u(i,j) = dForNewU(i,j) / sum(dForNewU(:,j));
        end
    end
    uf = u-uOld;
    sumuf=0;
    for i=1:c
        for j=1:pN(2)
            sumuf = sumuf + (uf(i,j)^2);
        end
    end
    check = sqrt(sumuf)
    
end

hold on
plot(x(1,:),x(2,:), '.', 'MarkerSize', 8)
plot(v(1,:),v(2,:), '*', 'MarkerSize', 8)

hold off


x(1,:)
x(2,:)
jVal
u
v
