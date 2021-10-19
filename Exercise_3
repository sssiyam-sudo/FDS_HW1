
# CODES FOR 3.a---------------------------------------------------------------------

def compute_histograms(image_list, hist_type, hist_isgray, num_bins):
  #####################################################
    image_hist = []
    for i in image_list:
        img=np.array(Image.open(i))
        
        if hist_isgray==True:
            img=rgb2gray(img.astype('double'))
        if hist_type == "grayvalue":
            image_hist.append(get_hist_by_name(img.astype('double'), num_bins, hist_type)[0])
        else:
            image_hist.append(get_hist_by_name(img.astype('double'), num_bins, hist_type))
 
  
  #####################################################
  
  return image_hist
  
  #----------------------------------------------------------------------------------
  
  def find_best_match(model_images, query_images, dist_type, hist_type, num_bins):
  
  #####################################################
    hist_isgray = is_grayvalue_hist(hist_type)
    
    model_hists = compute_histograms(model_images, hist_type, hist_isgray, num_bins) #lista di liste con gli istogrammi del modello
    query_hists = compute_histograms(query_images, hist_type, hist_isgray, num_bins) #lista di liste con gli istogrammi delle query
    
    D = np.zeros((len(model_images), len(query_images)))
    
    best_match=[]
    
    for i in range(len(model_hists)):
        for j in range(len(query_hists)):

            value=get_dist_by_name(model_hists[i],query_hists[j],dist_type)

            D[i,j]=value

    for j in range(len(query_hists)):
        bv=0
        mi=D[0,j]
        for i in range(len(model_hists)):
            if D[i,j]<mi:
                mi = D[i,j]
                bv=i
        best_match.append(bv)
        
  #####################################################  



#CODES FOR  3.b -------------------------------------------------------------------
#----------------------------------------------------------------------------------
def show_neighbors(model_images, query_images, dist_type, hist_type, num_bins):
  
  
  #####################################################
  num_nearest = 5  # show the top-5 neighbors
    best_match, D = find_best_match(model_images, query_images, dist_type, hist_type, num_bins)
    
    best_match=[]
    
    #look for the top-5
    for j in range(len(D[0])):
        mi=[]
        ok=[]
        
        for i in range(len(D)):
            if len(mi)==num_nearest:
                if mi[len(mi)-1][0]>D[i,j]:
                    mi.remove(mi[len(mi)-1])
                    mi.append([D[i,j],i,j])
                    
            else:
                mi.append([D[i,j],i,j])
            mi.sort()
        for elem in mi:
            ok.append(elem[1])
        best_match.append(ok)

    f, axarr = plt.subplots(1,num_nearest)
    for j in range(len(best_match)):

        modellini=[np.array(Image.open("./"+query_images[j]))]
        for i in range(len(best_match[j])):
            modellini.append(np.array(Image.open("./"+model_images[best_match[j][i]])))

        for immagini in range(len(modellini)):
            plt.subplot(1,num_nearest+1,immagini+1)
            plt.imshow(modellini[immagini])

        plt.show()
  #####################################################

  return best_match
  return best_match, D
