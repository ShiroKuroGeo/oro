Pagenated product in referral
public function index(Request $request)
{
    $perPage = 15; // Number of products per page
    $products = Product::paginate($perPage);

    return view('products.index', compact('products'));
}

@foreach ($products as $product)
    <div class="col-12 col-sm-6 col-md-4 col-xxl-2">
        <div class="product-card-container h-100">
            <div class="position-relative text-decoration-none product-card h-100">
                <div class="d-flex flex-column justify-content-between h-100">
                    <div>
                        <div class="border border-1 border-translucent rounded-3 position-relative mb-3">
                            <img class="img-fluid"
                                src="{{ asset('images/orotime-images/flyer1.jpg') }}"
                                alt="" />
                        </div>
                        <a class="stretched-link" data-bs-toggle="modal"
                            data-bs-target="#userId{{ $product->id }}" href="#">
                            <h6 class="mb-2 lh-sm line-clamp-3 product-name">
                                {{ $product->name }}
                            </h6>
                        </a>
                    </div>
                    <div>
                        <p class="fs-9 text-body-tertiary mb-2">{{ $product->category }}</p>
                        <div class="d-flex align-items-center mb-1">
                            <h3 class="text-body-emphasis mb-0">P{{ $product->price }}</h3>
                        </div>
                        <p class="text-body-tertiary fw-semibold fs-9 lh-1 mb-0">{{ $product->colors_count }} colors
                        </p>
                    </div>
                    <div class="modal fade" id="userId{{ $product->id }}"
                        aria-labelledby="userIdLabel" aria-hidden="true">
                        <div class="modal-dialog modal-dialog-centered">
                            <div class="modal-content">
                                <div class="modal-header">
                                    <h5 class="modal-title" id="userIdLabel">Save Referral Link</h5>
                                    <button type="button" class="btn-close"
                                        data-bs-dismiss="modal" aria-label="Close"></button>
                                </div>
                                <div class="modal-body">
                                    <small class="text-danger">Note: Copy the link inside the box.</small>
                                    <input type="text" name="referralLink"
                                    id="referralLink" disabled class="form-control"
                                    value="{{ Request::url() }}/{{ $product->id }}">
                                    <small class="text-danger">Note: You can only get your commission if someone is buying your referral.</small>
                                </div>
                                <div class="modal-footer">
                                    <button type="button" class="btn btn-secondary"
                                        data-bs-dismiss="modal">Close</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
@endforeach

<div class="d-flex justify-content-end">
    <nav aria-label="Page navigation example">
        {{ $products->links() }}
    </nav>
</div>
