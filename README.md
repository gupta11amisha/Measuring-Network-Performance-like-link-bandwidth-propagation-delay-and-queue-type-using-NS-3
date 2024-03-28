# Measuring-Network-Performance-like-link-bandwidth-propagation-delay-and-queue-type-using-NS-3
dataSize = 100:100:1000;
timeTaken = 10:10:100;
distance = 10:10:100;
speedOfLight = 299792:1:299802;
queueLength = 45;
threshold = 10:10:100;
Bandwidth = zeros(10);
propagationDelay = zeros(10);
answer = zeros(10);
queueType = cell(1,10);
throghput = zeros(10);
latency  = zeros(10);

for x = 1:10
    Bandwidth = (dataSize * 8) / (timeTaken(x) * 1000); 
end 

for y = 1:10
    propagationDelay = (distance * 1000) / (speedOfLight(y)-y+1);  
end

for x = 1:10
    if queueLength > threshold(x)
        queueType{x} = "Congested";
        answer(x) = 1;
    else
        queueType{x} = "Not Congested";
        answer(x) = 0;
    end
end

for i = 1:10
    latency = (dataSize * 8)/(Bandwidth(i) *1000);
end

for i = 1:10
    throughput = dataSize/timeTaken(i);
end

for i = 1:10
    jitter = latency/throughput(i);
end

disp('Bandwidth (kbps): ');
disp(Bandwidth);
disp('Propagation Delay (ms): ');
disp(propagationDelay);
disp('Queue Type: ');
disp(queueType);
disp("Latency (ms):");
disp(latency);
disp("Throughput");
disp(throughput);
disp("Jitter (bits/ms)");
disp(jitter);


subplot(4,1,1);
plot(Bandwidth, timeTaken);
xlabel('Bandwidth (kbps)');
ylabel('Time Taken');

subplot(4,1,2);
plot(propagationDelay, distance);
xlabel('Propagation Delay (ms)');
ylabel('Distance');

subplot(4,1,3);
stem(threshold, answer);
xlabel('Threshold');
ylabel('Queue Type');

subplot(4,1,4);
stem(latency, throughput);
xlabel('Latency');
ylabel('Throughput');

