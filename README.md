# Sorting-searching-
#include<iostream>
using namespace std;
void insertionSort(int *arr,int n)
{
    for(int i=1;i<n;i++)
    {
        int temp=arr[i];
        int j=i-1;
        while(j>=0 && arr[j]>temp)
        {
            arr[j+1]=arr[j];
            j--;
        }
        arr[j+1]=temp;
    }
}
void bubbleSort(int *arr,int n)
{
    for(int i=0;i<n-1;i++)
    {
        for(int j=0;j<n-i-1;j++)
        {
            if(arr[j+1]<arr[j])
            {
                swap(arr[j+1],arr[j]);
            }
        }
    }
}
void selectionSort(int *arr,int n)
{
    for(int i=0;i<n-1;i++)
    {
        int mini=i;
        for(int j=i+1;j<n;j++)
        {
            if(arr[mini]>arr[j])
            {
                mini=j;
            }
            
        }
        swap(arr[mini],arr[i]);
    }
}
void mergeTwoArray(int *arr,int s,int e)
{
    int mid=(s+e)/2;
    int len1=mid-s+1;
    int len2=e-mid;
    int *arr1=new int[len1];
    int *arr2=new int[len2];
    //copy the value to arr1
    int i=0;
    int mainArrayIndex=s;
    while(i<len1)
    {
        arr1[i++]=arr[mainArrayIndex++];
    }
    //copy the second value into arr2
    i=0;
   mainArrayIndex=mid+1;
    while(i<len2)
    {
        arr2[i++]=arr[mainArrayIndex++];
    }
    //merge 2 sorted array
    int index1=0;
    int index2=0;
    mainArrayIndex=s;
    while(index1<len1 && index2<len2)
    {
        if(arr1[index1]<arr2[index2])
        {
            arr[mainArrayIndex++]=arr1[index1++];
        }
        else{
            arr[mainArrayIndex++]=arr2[index2++];
        }
    }
    //remaing part left in arr1
    while(index1<len1){
        arr[mainArrayIndex++]=arr1[index1++];
    }
    //remaing part left in arr2
    while(index2<len2)
    {
        arr[mainArrayIndex++]=arr2[index2++];
    }
  delete []arr1;
  delete []arr2;
}
void mergeSort(int *arr,int s,int e)
{
    //base case
    if(s>=e)
    {
        return;
    }
    int mid=(s+e)/2;
    //left side sort
    mergeSort(arr,s,mid);
    //right side sort
    mergeSort(arr,mid+1,e);

    //mergesort two sorted array
    mergeTwoArray(arr,s,e);

}
int partitionElement(int *arr,int s,int e)
{
    int pivot=arr[s];
    int count=0;
    for(int i=s+1;i<=e;i++)
    {
        if(pivot>=arr[i])
        {
            count++;
        }
    }
    //right position in pivot
    int pivotIndex=count+s;
    swap(arr[pivotIndex],arr[s]);
    int small=s;
    int large=e;
    while(pivotIndex >small && pivotIndex <large)
    {
        while(arr[small]<pivot)
        {
            small++;
        }
        while(arr[large]>pivot)
        {
            large--;
        }
        if(pivotIndex > small && pivotIndex < large)
        {
            swap(arr[small++],arr[large--]);
        }

    }
return pivotIndex;
}
void quickSort(int *arr,int s,int e)
{
    if(s>=e){
        return;
    }
    
    //partition and do element in right position
    int partition=partitionElement(arr,s,e);

    quickSort(arr,s,partition-1);
    quickSort(arr,partition+1,e);
}
bool binary(int *arr,int n,int key)
{
    int s=0;
    int e=n-1;
    int mid=s+(e-s)/2;
    while(e>=s)
    {
        if(key==arr[mid]){
            return true;
        }
        else if(key>arr[mid])
        {
            s=mid+1;
        }
        else{
            e=mid-1;
        }
        mid=s+(e-s)/2;
    }
    return false;

}
bool linearSearch(int *arr,int size,int key)
{
    for(int i=0;i<size;i++)
    {
        if(arr[i]==key)
        {
            return true;
        }
    }
    return false;

}
int main()
{
    int arr[10]={10,23,34,45,56,67,79,89,90,99};
    bool b=binary(arr,10,99);
    bool l=linearSearch(arr,10,99);
    if(l)
    {
        cout<<"present element "<<endl;
    }
    else{
        cout<<"not present element "<<endl;
    }
    int data[10]={10,48,69,37,60,30,93,70,23,66};
    //insertionSort(data,10);
    //bubbleSort(data,10);
    //selectionSort(data,10);
    //mergeSort(data,0,10-1);
    //quickSort(data,0,10-1);
    for(int i=0;i<10;i++)
    {
        cout<<*(i+data)<<" ";
    }
}
